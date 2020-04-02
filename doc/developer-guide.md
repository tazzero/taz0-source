Developer Guide
===============

Setup
-----

    mkdir tazzero
    cd tazzero
    export SERVER=YOUR_SERVER_NAME
    rsync -avz -e ssh $SERVER:/home/web/taz0_cdn .
    git clone https://github.com/tazzero/taz0-cdn.git
    git clone https://github.com/tazzero/taz0-source.git
    cd taz0-source
    git clone https://github.com/tazzero/taz0-public.git
    mv taz0-public public
    cd ..

Result
------

    tree -L 1
    .
    ├── taz0_cdn
    ├── taz0-cdn
    └── taz0-source

-   `taz0_cdn` contains the real CDN data.
-   `taz0-cdn` the dummy CDN.
-   `taz0-source` the website source.
-   `taz0-source/public` the rendered website (it is the `taz0-public`
    repo).

Adding a new episode
--------------------

    cp CyperpunkBitstream-0xXX-NAME.mp3 taz0_cdn/static/cdn/cypherpunk-bitstream/
    touch taz0-cdn/static/cdn/cypherpunk-bitstream/CyperpunkBitstream-0xXX-NAME.mp3
    vi taz0-source/content/bitstream/0xXX-NAME.md
    cd taz0-source
    hugo serve
    hugo
    git add -v .
    git commit -m "add episode 0xXX"
    git push
    cd public
    git add -v .
    git commit -m "add episode 0xXX"
    git push
    cd ../../taz0-cdn
    git add -v .
    git commit -m "add episode 0xXX"
    git push
    rsync -avz -e ssh taz0_cdn/ $SERVER:/home/web/taz0_cdn
