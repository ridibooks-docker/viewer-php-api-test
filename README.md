# viewer-php-api-test

Docker image for tests of viewer's php-api based on PHP 7.x

## Supported Docker Images

* ridibooks/viewer-php-api-test:7.0 ([Dockerfile](https://github.com/ridibooks-docker/viewer-php-api-test/blob/master/7.0/Dockerfile)) - Docker image for tests of viewer's php-api based on PHP 7.0
* ridibooks/viewer-php-api-test:7.1 ([Dockerfile](https://github.com/ridibooks-docker/viewer-php-api-test/blob/master/7.1/Dockerfile)) - Docker image for tests of viewer's php-api based on PHP 7.1
* ridibooks/viewer-php-api-test:7.2 ([Dockerfile](https://github.com/ridibooks-docker/viewer-php-api-test/blob/master/7.2/Dockerfile)) - Docker image for tests of viewer's php-api based on PHP 7.2

## Test with Gitlab Runner

1. Download and install [gitlab-ci-multi-runner](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner)
2. Go to the project's directory that has `.gitlab-ci.yml` file.
3. Run `gitlab-runner exec ...` command like below:

```
# without SSH key
gitlab-runner exec docker [task_name]

# with SSH key
gitlab-runner exec docker [task_name] --env SSH_PRIVATE_KEY="`cat ~/.ssh/id_rsa`"
```
