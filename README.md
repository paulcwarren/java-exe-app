# Java Maven app to Use With `watchexec`

This is a Java Maven app WITHOUT Spring. Therefore, it can't use
spring-boot-devtools.

This is also not a true web app. It is a long-running process that prints "Hello
World!" to the console. Therefore, it can't use `.tanzu/wait.sh`

## Prerequisites
1. Run the most recent deploy script.
1. Make sure your `tilt` is up to date.
1. Make sure you have the Java Extension Pack installed in VSCode.
1. Clone this directory and open it in VSCode.

## Acceptance
1. `tilt up`.
1. Open the Tilt UI in the browser.
1. See that the resources go green.
1. At this point, the build will still be in progress. Track the build with `kp
   build logs sample-app-java-exe`. See that the `watchexec` buildpack is
   participating (in the `DETECT` phase), and that the default process type is
   `reload` (in the `EXPORT` phase). Wait for the build to complete.
1. Wait for the deployment pod (not the build pod) to be in the "Running" state. Only 1/2 containers
   will come up; this is okay.
1. In the Tilt UI, see the app print "Hello World!" every second.
1. In VSCode, make a change to `src/main/java/com/example/App.java` to make it
   print "Hello Tanzu!", and save.
1. In the Tilt UI, see that the container picked up the change to App.class and
   sync into the container. Within a second or two, the Tilt UI should show that
   the app is printing "Hello Tanzu!".
