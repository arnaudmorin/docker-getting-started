
Now that we've built an image, let's share it! To share Docker images, you have to use a Docker
registry. The default registry is Docker Hub and is where all of the images we've used have come from.

## Create a Repo

To push an image, we first need to create a repo on Docker Hub.

1. Go to [Docker Hub](https://hub.docker.com) and log in if you need to.

1. Click the **Create Repository** button.

1. For the repo name, use `getting-started`. Make sure the Visibility is `Public`.

1. Click the **Create** button!

If you look on the right-side of the page, you'll see a section named **Docker commands**. This gives
an example command that you will need to run to push to this repo.

![Docker command with push example](push-command.png){: style=width:75% }
{: .text-center }

## Pushing our Image

1. In the command line, try running the push command you see on Docker Hub. Note that your command
   will be using your namespace, not "YOUR-USER-NAME".

    ```plaintext
    $ docker push YOUR-USER-NAME/getting-started
    Using default tag: latest
    The push refers to repository [docker.io/YOUR-USER-NAME/getting-started]
    tag does not exist: YOUR-USER-NAME/getting-started:latest
    ```

    Why did it fail? The push command was looking for an image named docker/getting-started using the default `latest` tag, but
    didn't find one. If you run `docker image ls`, you won't see one either.

    To fix this, we need to "tag" our existing image we've built to give it another name.

1. Login to Docker Hub by either clicking on the "Sign In" button in Docker Desktop or using the 
   command `docker login -u YOUR-USER-NAME`.

1. Use the `docker tag` command to give the `getting-started` image a new name. Be sure to swap out
   `YOUR-USER-NAME` with your Docker ID.

    ```bash
    docker tag getting-started YOUR-USER-NAME/getting-started
    ```

1. Now try your push command again. If you're copying the value from Docker Hub, you can drop the 
   `tagname` portion, as we didn't add a tag to the image name. If you don't specify a tag, Docker
   will use a tag called `latest`.

    ```bash
    docker push YOUR-USER-NAME/getting-started
    ```

## Recap

In this section, we learned how to share our images by pushing them to a registry. We can now run this
brand new image from anywhere! This is quite common in CI pipelines,
where the pipeline will create the image and push it to a registry and then the production environment
can use the latest version of the image.

Now that we have that figured out, let's circle back around to what we noticed at the end of the last
section. As a reminder, we noticed that when we restarted the app, we lost all of our todo list items.
That's obviously not a great user experience, so let's learn how we can persist the data across 
restarts!
