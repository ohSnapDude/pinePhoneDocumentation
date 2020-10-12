# Geary

Geary is an email client written with the GTK UI. The package itself is already present in the alpine linux repos, however this version is not up to date and does not scale properly. According to [linuxOnMobile](https://linmob.net/2020/07/31/pinephone-daily-driver-challenge-part3-reading-apps-and-email.html#special-email), there are builds coming out for mobian os which have this proper scaling. He also had a theory that grabbing the source itself and building it would have this scaling... and it does!

**NOTE:** This guide is incomplete, there is some troubleshooting left to do. According to [The postmarketOs mastadon](https://fosstodon.org/@postmarketOS/104978710529782231) the setup wizard is not optimized for smaller screens at this time on postmarketOs. If getting a working build is possible we could go places!
As of this writing there is some troubleshooting to be done as the build doesn't recognize the email database and winds up having an async crash.

In general this page is a work in progress.

## Build

I did not test building this without [docker this time](./dockerSetup.md). However I would highly recommend it because you can throw away the docker instance if this is all you need to build.

Install the following in the environment:

```apk add samurai meson webkit2gtk-dev sqlite-dev vala gmime-dev desktop-file-utils iso-codes-dev itstool gettext appstream-glib-dev enchant2-dev folks-dev gspell-dev libhandy-dev libpeas-dev libunwind-dev ytnef-dev```

clone the repository:

`https://source.puri.sm/Librem5/geary.git`

enter the directory and run the following commands:

`meson build`

`ninja -C build`

After geary is build, you will need this package on your target phone to run:

`sudo apk add libunwind`

## Troubleshoot

Unfortunately despite these steps I cannot get geary to run properly. Geary recognizes the email address but it appears as if there are database errors:

```txt
Account identifier: account_01
Account provider: GEARY_SERVICE_PROVIDER_OUTLOOK
Error type: GearyEngineError 11
Message: /home/user/.local/share/geary/account_01/geary.db schema 25 unknown to current schema plan

Back trace:
 * geary_error_context_new
 * geary_problem_report_construct
 * geary_account_problem_report_construct
 * geary_account_problem_report_new
 * application_controller_open_account_co
 * application_controller_open_account_ready
 * g_subprocess_communicate_utf8
 * g_task_attach_source
 * geary_imap_engine_generic_account_real_open_async_co
 * geary_imap_engine_generic_account_open_async_ready
 * g_subprocess_communicate_utf8
 * g_task_attach_source
 * geary_imap_engine_generic_account_internal_open_async_co
 * geary_imap_engine_generic_account_internal_open_async_ready
 * g_subprocess_communicate_utf8
 * g_task_attach_source
 * geary_imap_db_account_open_async_co
 * geary_imap_db_account_open_async_ready
 * g_subprocess_communicate_utf8
 * g_task_attach_source
 * geary_imap_db_database_open_co
 * geary_imap_db_database_open_ready
 * g_subprocess_communicate_utf8
 * g_task_attach_source
 * geary_db_versioned_database_real_open_co
 * geary_db_versioned_database_open_ready
 * g_subprocess_communicate_utf8
 * g_task_attach_source
 * geary_db_versioned_database_exists_co
 * geary_db_versioned_database_exists_ready
 * g_subprocess_communicate_utf8
 * g_subprocess_communicate_utf8
 * g_main_context_dispatch
 * g_main_context_dispatch
 * g_main_context_iteration
 * g_application_run
 * _vala_main
 * main
 * _init
 * _init
```

Trying to figure out right now if this has to do with the `-DSQLITE_ENABLE_FTS3` build flag. However I didn't build sqlite from source so I'm not sure if that's the case.

At the moment this is where the story ends