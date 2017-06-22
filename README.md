# Ansible Laws

The main purpouse of this document is to define a guide of **Best Practices**
that should be adopted when building huge automation projects in *Ansible*.
As the things can run wild when teams start scripting tasks (each one doing the
things on its way), we found necessary to define some **Rules of Convenience**
to be followed by everyone involved, so the things can be set in a little more
stable shape.
________________________________________________________________________________

## The 10 Commandments

Follow this and you will be happy. Seriously.

### 1. I am the tool for automation, configuration and provisioning
  - Use *Ansible* to automate complicated or recurrent tasks
  - Use *Ansible* to change configuration values on devices or applications
  - Use *Ansible* for provisioning new environments

### 2. Thou shalt think before start writing
  - Plan the tasks you need to automate
  - Plan how to make them reusable
  - Share your plans with your team
  - Make the necessary changes
  - Count to 10 and start writing

### 3. Thou shalt use Roles
  - What you'll do can be reused? Pick a `role`;
  - The `role` doesn't yet exist? Create a new one;
  - The new `role` is generic and can be reused? No? So, change it!

### 4. Thou shalt always choose Modules in the right order
  When you need a module, start looking for:
  - Official (`ansible-modules`)
  - Extra (`ansible-modules-extra`)
  - Community (modules maintained by community)
  If you have not found what you want, you can:
  - Contribute (help evolving an existing **official**, **extra** or **community** module)
  - Create (yes, make your own `module.py`)
  - Use `shell`/`command`/`raw` modules (the least priority; use **only** when **EXTREMELLY necessary**)

### 5. Thou shalt not use fixed values in Playbooks and Roles
  - When possible, never fix values inside of a `playbook`
  - The same is valid for the `roles`
  - Use `variables`, that can be passed by the user from outside
  - Variables can be passed from a large variety of places and files
  - Variables are cool ;)

### 6. Thou shalt not use files when templates could be used
  - Some files are static, and it's OK to copy them just as they are
  - But a lot of files has configurations and settings - and they can change
  - Use **jinja2** to create template files (`file.j2`)
  - Use `template` module for templating tasks

### 7. Remember the Idempotence
  - Running a `playbook` should define a desired **state**
  - Running the same `playbook` again should still guarantee the same **state**
  - Running the same `playbook` again² should still guarantee the same **state**
  - Running the same `playbook` again³ should still guarantee the same **state**
  - Yeah, I think you got it...

### 8. Honour thy community
  - When you create a new `module`, share it with the community
  - This way you help other people, and they can even improove your job
  - Remember that you are using modules that they brought to you

### 9. Ye shall TEST
  - When you first create a `playbook`, you need to test it
  - When you first create a `role`, you need to test it
  - When you first create a `module`, you need to test it
  - When you change anything, you need to **test it all again**
  - Do automatic unitary tests
  - Do automatic recursive tests

### 10. Ye shall DOCUMENT
  - Document `playbooks`
  - Document `roles`
  - Document `modules`
  - Document `variables`
  - Document all, even the `inventories`
  - And... Are you changing something? Do _document_! Your team isn't always aware of what you've done.

