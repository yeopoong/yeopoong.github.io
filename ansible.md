Ansible
=======

Ansible 설치 
------------

```
$ apt-get install ansible 
```

쿡북 생성
--------

>$ /etc/ansible/hosts  

>$ cd chef-repo  
>$ knife cookbook create hello -o cookbooks  

레시피 편집
----------

>$ vi cookbooks/hello/recipes/default.rb  

```ruby
#
# Cookbook Name:: hello
# Recipe:: default
#   
# Copyright 2016, YOUR_COMPANY_NAME
#
# All rights reserved - Do Not Redistribute
#
log "Hello, Chef!"
```

`localhost.json`
```json
{
    "run_list" : [
        "recipe[hello]"
    ]
}
```

`solo.rb`
```ruby
file_cache_path "/tmp/chef-solo"
cookbook_path ["/home/ec2-user/chef-repo/cookbooks"]
```

>$ sudo chef-solo -c solo.rb -j localhost.json  
  

