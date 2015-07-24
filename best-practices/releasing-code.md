# Releasing Code

Fusion maintains a [number of open source projects](../team-culture/open-source.md). We tag releases [following semantic versioning](http://semver.org/), and value regular releases over those packed with features. This is our guide to tagging releases.

## Leading up to the release

In the week or so leading up to a release, here are the steps you'll likely want to perform:

* Make sure all closed issues and merged pull requests are assigned to the appropriate milestone. For those coming back to the project at a later date, this is tremendously helpful when trying to figure out what was changed in a release.
* Update screenshots (as necessary). Capture core functionality and admin screens (if applicable). 
* For WordPress plugins, the screenshots need to follow the format of `screenshot-[\d]+.(jpg|png|gif)` in the project root. This is how WordPress.org will know which screenshots to display.
* For any other projects, screenshots can live in a subdirectory and be linked to from the readme.
* Update documentation (as necessary). Capture configuration details for new features and API changes. It can also be a good opportunity to edit for clarity. A good way to begin documentation efforts is setting up the plugin in a clean install of WordPress. Approach the problem with fresh eyes.
* Update the changelog with all improvements and bug fixes for the release. For WordPress plugins, the changelog lives in `readme.txt`. Non-WP projects should have `CHANGELOG.md` in their project root.
* Draft the release post.
* Outline a promotion plan for the release post.

It's helpful if these tasks are delegated between a couple of people.

## Tagging a release

When you're ready to push the release live, here's what you'll want to do:

* Do a final read through of the readme, changelog and any other written documentation.
* Tag the release version through Github's web interface. Ideally, you'll copy and paste the changelog into the release notes. Tagging a release through the web UI will result in a new Git tag being created.
* Publish release post on Fusion.net.
* Execute the promotion plan.

## Post-release

Following up a couple to a few days after release can be a help kick-start to the next interation on the project:

* Evaluate promotion plan.
* Stub a Trello card with the next scheduled release.
* Capture any lessons learned during the development of the release.

## WordPress plugins

Our WordPress plugins require a few additional steps for each release:

* Run `grunt i18n` to generate the freshest POT (translation) files.
* Run `grunt readme` to compile `readme.md` from `readme.txt`. `readme.txt` is always the canonical readme.
* Ship tagged release to WordPress.org (if the plugin was submitted to the plugin directory).
* If you are not already watching the plugin, subscribe to the WordPress support forum posts for the plugin. Visit the plugin's support page at `https://wordpress.org/support/plugin/{plugin-slug}`, and there are RSS and email subscription links.
