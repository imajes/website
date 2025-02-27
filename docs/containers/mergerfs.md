<div class="image-logo"><img src="/img/image-logos/mergerfs.svg" alt="logo"></div>

[:octicons-mark-github-16: GitHub](https://github.com/hotio/mergerfs){: .header-icons target=_blank rel="noopener noreferrer" }  
[:octicons-container-16: docker.io](https://hub.docker.com/r/hotio/mergerfs){: .header-icons target=_blank rel="noopener noreferrer" }
 / [:octicons-container-16: ghcr.io](https://github.com/orgs/hotio/packages/container/package/mergerfs){: .header-icons target=_blank rel="noopener noreferrer" }
 / [:octicons-container-16: quay.io](https://quay.io/repository/hotio/mergerfs){: .header-icons target=_blank rel="noopener noreferrer" }  
[:octicons-link-16: MergerFS](https://github.com/trapexit/mergerfs){: .header-icons target=_blank rel="noopener noreferrer" }  

--8<-- "includes/stats.md"

## Starting the container

!!! docker ""

    === "cli"

        ```shell
        docker run --rm cr.hotio.dev/hotio/mergerfs ...
        ```

The default `ENTRYPOINT` is `mergerfs -f`.

--8<-- "includes/tags.md"

## Using the mergerfs mount on the host

By setting the `bind-propagation` to `shared` on the volume `mountpoint`, like this `-v /data/mountpoint:/mountpoint:shared`, you are able to access the mount from the host. If you want to use this mount in another container, the best solution is to create a volume on the parent folder of that mount with `bind-propagation` set to `slave`. For example, `-v /data:/data:slave` (`/data` on the host, would contain the previously created volume `mountpoint`). Doing it like this will ensure that when the container creating the mount restarts, the other containers using that mount will recover and keep working.

## Extra docker privileges

In most cases you will need some or all of the following flags added to your command to get the required docker privileges when using a mergerfs mount.

```shell
--security-opt apparmor:unconfined --cap-add SYS_ADMIN --device /dev/fuse
```
