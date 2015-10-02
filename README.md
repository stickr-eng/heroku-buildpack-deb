# Heroku Deb Buildpack

This is a heroku custom buildpack that downloads, unpacks, and copies static
binaries from .deb files.

## Usage

Add a 'debs.txt' file to the root of your project. Add deb files, one per line,
with fields pipe-separated. The fields are

1. name
2. .deb. url
3. sha1sum of .deb file

Example:

    wkhtmltopdf|http://download.gna.org/wkhtmltopdf/0.12/0.12.2.1/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb|5c509de79121e96908794ebcb9d16647a9385e1d

Add the buildpack to your stack of packs. Pick the index so that it is NOT the
final buildpack.

    heroku buildpacks:add https://gitlab.com/stickr/heroku-buildpack-deb.git -i 2

Release the app and see what happens!


## Testing

You can test your config by cloning this repo and running it locally:

    mkdir build
	curl YOUR_DEB_URL -o build/your_deb_name.deb
	sha1sum build/your_deb_name.deb
	vi build/debs.txt   # Set up your config
	bin/compile build   # Test it

Once you have that working, do one final run all the way through:

    rm build/*.deb
	bin/compile build


## TODO

1. Cache download and/or binaries in the cache dir.
2. Handle non-static binaries

