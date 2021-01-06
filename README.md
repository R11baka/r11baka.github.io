# r11baka.github.io
My simple blog.For fun
## How to run
docker run --rm -it --volume="$PWD:/srv/jekyll" -p 3000:4000 --volume="$PWD/vendor/bundle:/usr/local/bundle" --env JEKYLL_ENV=production jekyll/jekyll:3.8 jekyll serve
