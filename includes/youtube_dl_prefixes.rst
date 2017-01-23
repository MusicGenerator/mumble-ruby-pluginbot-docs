This is a string that will prefix the youtube_dl shell command. You can set anything that would work on a shell. This can for example be used to renice the youtube_dl command.

If youtube_dl command is ``youtube-dl foo bar`` and ``plugin:name_of_your_plugin:youtube_dl:prefixes`` is ``nice -n 19`` then the full command results in::

    nice -n19 youtube-dl foo bar
