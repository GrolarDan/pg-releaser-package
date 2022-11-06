# PG Releaser Package

Template application for packaging self-contained Java application.

`jpackage.txt` and `jpackage.properties` files are used for testing of jpackage tool directly

```shell
  jpackage --add-launcher DMK=jpackage.properties "@jpackage-windows-latest.txt"
```

The macOS JPackage has restriction for the version

**Bundler Mac DMG Package skipped because of a configuration problem: The first number in an app-version cannot be zero or negative.**  

## Test JPackage locally

set environment variables for signing

* Find your key-id (using  `gpg --list-secret-keys --keyid-format=long` )
* Export the gpg secret key to an ASCII file using `gpg --export-secret-keys -a  > secret.txt`
* Export public key to file `gpg --export -a -o public.txt`
* Export secret key to file `gpg --export-secret-keys -a -o secret.txt`

```shell
  gpg --list-secret-keys --keyid-format=long
  gpg --export -a -o public.txt <key-id>
  gpg --export-secret-keys -a -o secret.txt <key-id>
  # windows
  set JRELEASER_GPG_PUBLIC_KEY=public.txt
  set JRELEASER_GPG_SECRET_KEY=secret.txt
  set JRELEASER_GPG_PASSPHRASE=%GPG_PASSPHRASE%
  # linux
  export JRELEASER_GPG_PUBLIC_KEY=public.txt
  export JRELEASER_GPG_SECRET_KEY=secret.txt
  export JRELEASER_GPG_PASSPHRASE=%GPG_PASSPHRASE%
```

Run only assemble
```shell
  mvn clean package -Passemble -Drevision=1.0.0
```

Run 
```shell
  set JRELEASER_SIGNING_MODE=FILE
  export JRELEASER_SIGNING_MODE=FILE
  mvn clean deploy -Passemble -Prelease -Drevision=1.0.0 -Djreleaser.dry.run=true -Djreleaser.signing.mode=FILE
```