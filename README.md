# RHCSA 8 Lab Environment

## About

This repo contains a lab environment used for RHCSA training.

## Systems

- `server1`:
   - OS: CentOS 8
   - IP: `192.168.0.110`

- `server2`:
   - OS: CentOS 8
   - IP: `192.168.0.120`

## Dependencies

- [Virtualbox](https://www.virtualbox.org)
- [Vagrant](https://www.vagrantup.com)

## Get started:

```
$ git clone https://github.com/skingry/lab-environment.git

$ cd lab-environment
```

## Startup:

- Start all servers:

```
$ vagrant up
```

- Start a specific server:

```
$ vagrant up $MACHINE_NAME
```



## Accessing the systems:

- To get shell access to a specific system:

```
$ vagrant ssh $MACHINE_NAME
```

Replace `$MACHINE_NAME` with either `server1` or `server2`...

## Shutdown:

- Stopping all systems:

```
$ vagrant halt
```

- Stopping a specific system:

```
$ vagrant halt $MACHINE_NAME
```

Replace `$MACHINE_NAME` with either `server1` or `server2`...

## Reset all the things

```
$ vagrant destroy
```

## System Credentials:

| System | IP | $ | password | # | password |
|---|---|:---:|:---:|:---:|:---:|
|`server1`|192.168.0.110|`user1`|`password`|`root`|`password`|
|`server2`|192.168.0.120|`user1`|`password`|`root`|`password`|
