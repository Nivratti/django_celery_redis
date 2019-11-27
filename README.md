***************************
django_celery_redis
***************************

Project to demonstrate celery and redis for distributed message queue

Redis is an in-memory key-value store known for its flexibility, performance, and wide language support. This tutorial demonstrates how to install, configure, and secure Redis on an Ubuntu 18.04 server.

## Step 1 — Installing and Configuring Redis

In order to get the latest version of Redis, we will use apt to install it from the official Ubuntu repositories.
Update your local apt package cache and install Redis by typing:

``` console
$ sudo apt update
$ sudo apt install redis-server
```

This will download and install Redis and its dependencies. Following this, there is one important configuration change to make in the Redis configuration file, which was generated automatically during the installation.

Open this file with your preferred text editor:

```console
sudo nano /etc/redis/redis.conf
```

Inside the file, find the supervised directive. This directive allows you to declare an init system to manage Redis as a service, providing you with more control over its operation. The supervised directive is set to no by default. Since you are running Ubuntu, which uses the systemd init system, change this to systemd:

# /etc/redis/redis.conf

```
. . .

# If you run Redis from upstart or systemd, Redis can interact with your
# supervision tree. Options:
#   supervised no      - no supervision interaction
#   supervised upstart - signal upstart by putting Redis into SIGSTOP mode
#   supervised systemd - signal systemd by writing READY=1 to $NOTIFY_SOCKET
#   supervised auto    - detect upstart or systemd method based on
#                        UPSTART_JOB or NOTIFY_SOCKET environment variables
# Note: these supervision methods only signal "process is ready."
#       They do not enable continuous liveness pings back to your supervisor.
supervised systemd
```

That’s the only change you need to make to the Redis configuration file at this point, so save and close it when you are finished. Then, restart the Redis service to reflect the changes you made to the configuration file:

```
sudo systemctl restart redis.service
```

## Step 2 — Testing Redis

As with any newly-installed software, it’s a good idea to ensure that Redis is functioning as expected before making any further changes to its configuration. We will go over a handful of ways to check that Redis is working correctly in this step.

Start by checking that the Redis service is running:

```console
sudo systemctl status redis
```

To test that Redis is functioning correctly, connect to the server using the command-line client:\

```console
redis-cli
```

In the prompt that follows, test connectivity with the ping command:

```console
ping
```

```
Output
PONG
```

Original link <https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-redis-on-ubuntu-18-04>_


