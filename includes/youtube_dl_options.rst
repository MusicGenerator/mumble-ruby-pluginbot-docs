With this string you can add options/parameters to the executed youtube_dl shell command.

If youtube_dl command is ``youtube-dl foo bar`` and ``plugin:name_of_your_plugin:youtube_dl:options`` is ``--restrict-filenames`` then the full command results in::

    youtube-dl --restrict-filenames foo bar
