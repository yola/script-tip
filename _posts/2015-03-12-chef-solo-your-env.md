---
layout: post
title: "Preparing your env ready for chef-solo"
---

## Preparing your env for chef-solo

I've written some shell functions to mostly automate
(and serve as a reminder of what I did in the first place)
preparing a dev server for running chef solo.

```bash
#  knife role show yola_base -F json >! roles/yola_base.json
function rolejson() {
    knife role show $1 -F json
}

CHEF_DIR="${YOLA_SRC}/chef"

function rolestojson() {
    ROLESPATH="${CHEF_DIR}/roles"
    ROLES=($(find ${ROLESPATH} -name '*.rb'))
    (( count = 0 ))
    for i in ${ROLES}; do
        n="${i:t:r}"
        (( count = count + 1 ))
        echo "${n} [${count}/${#ROLES}]"
        rolejson "${n}" >! "${ROLESPATH}/${n}.json"
    done
}

function chefmyenv() {
    ENV=${1:-default.env.name.here}
    rolestojson
    cat >! ${CHEF_DIR}/solo.rb <<EOF
role_path "/home/user/chef/roles"
environment_path "/home/user/chef/environments"
cookbook_path ["/home/user/chef/cookbooks", "/home/henk/chef/external-cookbooks"]
data_bag_path "/home/user/chef/data_bags"

EOF
    rsync --delete-after -av ${CHEF_DIR} ${ENV}:
    ssh ${ENV} "sudo cp chef/solo.rb /etc/chef/solo.rb"
    rm ${CHEF_DIR}/solo.rb
}
```

With these functions sourced, you should be able to simply `chefmyenv`, then `ssh` into it and run `sudo chef -z -c /etc/chef/solo.rb -l info -j path/to/node.json`

