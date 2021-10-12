# Releasing Moodle plugins in the Plugins directory automatically from Gitlab with Gitlab-CI

## Usage
1. Make sure you add the variable MOODLE_ORG_TOKEN to the repo variables in the Gitlab settings. You can retrieve this value from https://moodle.org/plugins (click API access when logged in).
2. Copy the .gitlab-ci.yml file over to your repo.
3. Edit the .gitlab-ci.yml file to make sure the env variables are correct. At this time, this is only the `PLUGIN` variable.
4. That's it! Now when you tag the repository with a tag that matches the configured condition, the tagged version will be released in the plugins directory.

By default, this is configured to do as follows:
1. Run all tests for specified versions, the subcalls which have `|| true` will not cause failures. Use this with caution.
2. Create a release in Gitlab.
3. Create a release in Moodle.org.

## Tips

* Use settings `$plugin->requires`, `$plugin->supported` and
  `$plugin->incompatible` in your plugin's
  [version.php](https://docs.moodle.org/dev/version.php). They are used to
  automatically populate the list of supported Moodle versions. By default, all Moodle
  versions starting from the one described by `$plugin->requires` will be marked as
  supported.
* Keep the `CHANGES.md` file in the root of your repository. It will be automatically
  imported as release notes for the new version. Please see [Moodle dev
  docs](https://docs.moodle.org/dev/Plugin_files#CHANGES) for all supported names and
  formats.

## License

This program is free software: you can redistribute it and/or modify it under the
terms of the GNU General Public License as published by the Free Software Foundation,
either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this
program. If not, see <http://www.gnu.org/licenses/>.


## References
The idea of this was created from https://github.com/moodlehq/moodle-plugin-release, which is similar, but for Github.
