## Ignore Host Key Checking

If you understand the implications and wish to disable this behavior, you can do so by editing /etc/ansible/ansible.cfg or ~/.ansible.cfg:

[defaults]
host_key_checking = False

Alternatively this can be set by an environment variable:

$ export ANSIBLE_HOST_KEY_CHECKING=False

## Logging

Ansible will log some information about module arguments on the remote system in the remote syslog, unless a task or play is marked with a “no_log: True” attribute. This is explained later.

## Types of connection

ansible_connection=
	local
	docker
	ssh
	paramiko
	smart


## Adding hosts to inventory during playbook

- name: add container to inventory
  add_host:
    name: my_jenkins
    ansible_connection: docker
    ansible_docker_extra_args: "--tlsverify --tlscacert=/path/to/ca.pem --tlscert=/path/to/client-cert.pem --tlskey=/path/to/client-key.pem -H=tcp://myserver.net:4243"
    ansible_user: jenkins
  changed_when: false

## Patterns

### All

all
*

### Ungruped?

### Host(s)

one.example.com
one.example.com:two.example.com
192.0.2.50
192.0.2.*

### Group

webservers

### OR

webservers:dbservers

### NOT (exclude)

webservers:!phoenix

### AND (intersection)

webservers:&staging

### With variables (uncommon)

webservers:!{{excluded}}:&{{required}}

### Wildcards

*.example.com
*.com

### Combinations

webservers:dbservers:&staging:!phoenix
one*.com:dbservers

### By position

webservers[0]       # == cobweb
webservers[-1]      # == weber
webservers[0:1]     # == webservers[0],webservers[1]
                    # == cobweb,webbing
webservers[1:]      # == webbing,weber

### Regex (uncommon)

~(web|db).*\.example\.com

## Limiting

ansible-playbook site.yml --limit datacenter2
ansible-playbook site.yml --limit @retry_hosts.txt

## Using SSH Keys (???)

ssh-agent bash
ssh-add ~/.ssh/id_rsa

## Forking (paralelism)

ansible atlanta -a "/sbin/reboot" -f 10

Change settings in Ansible's configuration file

## Transfering files

ansible atlanta -m copy -a "src=/etc/hosts dest=/tmp/hosts"

## Background and Poll

ansible all -B 1800 -P 60 -a "/usr/bin/long_running_operation --do-stuff"

-B 3600 => 30 minutes timeout
-P 30 => Poll for status each 60 seconds

ansible web1.example.com -m async_status -a "jid=488359678239.2844"

## Useful Ansible configurations (config file)

display_args_to_stdout = True
error_on_undefined_vars = True
forks = 5
gathering = smart




