= Doko.js

A tool for finding out which javascript file:line inserted a DOM element. Helpful for situations where you're new to a codebase and you see a UI element and you want to know where it came from.

Only works with javascript/jquery apps.

== Installation

Copy the doko.js file and paste in your `public` directory or one that your web server has access to.

Dojo.js needs to run before any other scripts, so place it on the very top before the others.

    <script src="doko.js"></script>

Also, depending which library you're using, you may need to specify external libraries you wish to prevent from showing up as a potential source location. This is because of the way we track the origin of client-side DOM insertion. In order to do that, put a `data-orig-exclude-list` attribute in the `<head>` tag, and list a comma separated names of libraries you want to exclude.

    <head data-orig-exclude-list="jquery,backbone">

The reason why you may need to do this is because of the way we track the javascript file:line. We intercept the native DOM insertion methods such as `appendChild`, `insertBefore`, or `replaceChild`, look at the stacktrace, and then go through it to find the most recent caller which corresponds to our javascript code.

