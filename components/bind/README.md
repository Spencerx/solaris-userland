Copyright (c) 2022, 2023, Oracle and/or its affiliates.

# BIND notes.

These notes are for engineering only.  They are not distributed with
the packaging but are available with the source code.

## BIND compatibility

BIND 9 configuration (named.conf) during a micro version update should
remain compatible.  And indeed for the most part between minor version
updates too; some features might no longer work but the keywords are
ignored.

BIND source has three major branches, Stable, Extended Support Version
(ESV), and development. As of BIND 9.13, the minor odd number is the
Development version which may receive new features at each micro
version.  While even numbered version remain stable, receiving only
bug fixes and no new features.

The three current branches are

- 9.16.x Current-Stable, ESV
- 9.18.x Current-Stable, ESV, including OpenSSL 3.0 support.
- 9.19.x Development version

## Packaging

- bind.p5m (pkg:/service/network/dns/bind)
- bindc.p5m (pkg:/network/dns/bind)

### bind.p5m - Server package

Provides BIND server (in.named), server specific tools, and SMF
features.

When the BIND server package is updated it logs a short note as the
full instructions are rather long.
The short note is located in ./Solaris/bind-notice.txt,
which following an update is also viewable
via `pkg history` command.
The source of the longer note is in ./Solaris/bind-transition.txt.

The short note is delivered as
usr/share/doc/release-notes/bind-update.txt, and includes attribute
*self@$(IPS\_COMPONENT\_VERSION)* causing it to be displayed when the
component version is incremented.

By specifying the version as IPS\_COMPONENT\_VERSION the
release-note will correctly be applied when BIND component is
updated, and COMPONENT\_VERSION is modified in Makefile.  As
updates do not have to be applied incrementally it is not possible
to use the version as a definitive comparison to the
compatibility.

### bindc.p5m - Client Package
Provides DNS tools, utilities, manual pages and libraries.


## Testing

### Makefile testing

`gmake test` runs a very simple set of tests by executing
./Solaris/testing.ksh.

`gmake test-version` Runs `named -V` which shows its version number
and additional library, compiler, and configuration information.

### Full testing

To run the full testing provided by BIND the machine needs to be
configured with a dozen or so loop-back IP addresses in the 10.53.x.y
range.  A script is provided to configure those addresses but you
obviously need root access (or sufficient privileges) to add those.
It is possible therefore to run the test where you have root access,
either on your own build machine or a suitably configured machine
where you have re-created the build machines directory structure and
copied "build" and the source directory over.

Note that these test will not run when executed by root.

For example

1. Create tar ball of build and source directory.

	```
	$ cd $(hg root)/components/bind
	$ pwd
	/builds/user/workspace/components/bind
	$ tar zcf ~/test.tar.gz build bind-9.16.29
	$
	```

2. ON your test machine, create directory structure to mimic that of
   the build machine.

	```
	$ WS=/builds/user/workspace
	$ sudo mkdir -p $WS
	$ sudo chown $USER $WS
	$ mkdir -p $WS/components/bind
	```

3. Unpack tar ball from build machine

	```
	$ cd $WS/components/bind
	$ tar zxf ~/test.tar.gz
	```

4. Change to architecture directory, configure the interfaces.

	```
	$ cd build/amd64 || cd build/sparcv9
	$ cd bin/tests/system
    $ sudo ifconfig.sh up
	```

5. Set PATH so that GNU utilities are used, unset http\_proxy and
   execute test.

	```
    $ PATH=/usr/gnu/bin:/usr/bin:/usr/sbin; export PATH
	$ unset http_proxy
    $ sh runall.sh
	```

6. Optional, run individual test or a bunch of tests using 'run.sh':

   ```
   $ sh run.sh doth acl addzone
   ```

The tests may take some hours to complete.  They write a summary
report to ./build/*/bin/tests/system/systests.output.

For further information regarding these tests refer to README in
bin/tests/system directory.  The test framework is changing to use
pytest.  As per the README the older testing can still be used using
the legacy scripts.  A helper script in ./Solaris/test-summarize.awk
can help examine the summary report from the legacy scripts, for
example to review a summary of skipped tests:

```
awk -v skipped=1 -f $WS/components/bind/Solaris/test-summarize.awk \
   ./bin/tests/system/systests.output

```


### Skipped tests

Some of tests require additional software to be installed, such as
`dnspython` and Perl modules `Net::DNS` and `Digest-HMAC`.

With those packages installed currently a total of three tests are
skipped which rely on options not currently configured:

- SKIP: engine_pkcs11
- SKIP: geoip2
- SKIP: keyfromlabel


### Failed tests

- serv-stale fails to initialise.
- tsig requires Net::DNS (Should have been skipped)

