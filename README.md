# andOTP - Android OTP Authenticator

[![Build Status](https://git.private.coffee/PrivateCoffee/andOTP/badges/workflows/deploy_snapshot.yml/badge.svg)](https://git.private.coffee/PrivateCoffee/andOTP/actions)
[![Latest Commit](https://shields.private.coffee/gitea/last-commit/PrivateCoffee/andOTP?gitea_url=https%3A%2F%2Fgit.private.coffee)](https://git.private.coffee/PrivateCoffee/andOTP)
[![Chat - Matrix](https://shields.private.coffee/badge/chat-Matrix-blue.svg)](https://matrix.pcof.fi/#/#general:private.coffee)

![andOTP](https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/logo.png)

## Intro

andOTP is a two-factor authentication App for Android 5.1+.

It implements Time-based One-time Passwords (TOTP) and HMAC-Based One-Time Passwords (HOTP).
Simply scan the QR code and login with the generated 6-digit code.

This project started out as a fork of the great [OTP Authenticator](https://github.com/0xbb/otp-authenticator) app written by [Bruno Bierbaumer](https://github.com/0xbb),
which has sadly been inactive since 2015. By now almost every aspect of the app has been changed/re-written so the fork status of the Github repository got
detached upon [user request](https://github.com/andOTP/andOTP/issues/145). But all credit for the original version and for starting this project still goes to Bruno!

### Fork Information

This is a fork of the [original andOTP project](https://github.com/andOTP/andOTP) by [Jakob Nixdorf](https://github.com/flocke), which is no longer maintained. This fork is maintained by [Private.coffee](https://private.coffee) and aims to keep the app up-to-date with the latest Android versions. It is not as thoroughly tested as the original app, so please report any issues you encounter.

All commits on the main branch trigger a build of an APK, which is uploaded to the [Private.coffee Git](https://git.private.coffee/PrivateCoffee/-/packages/generic/andotp/latest). To migrate from the original andOTP app, please create a backup of your data using the original app and restore it using this fork.

## Features:

- Free and Open-Source
- Requires minimal permissions
  - Camera access for QR code scanning
  - Storage access for import and export of the database
- Encrypted storage with two backends:
  - Android KeyStore
  - Password / PIN
- Multiple backup options:
  - Plain-text
  - Password-protected
  - OpenPGP-encrypted
- Sleek minimalistic Material Design with three different themes:
  - Light
  - Dark
  - Black (for OLED screens)
- Great Usability
- Compatible with Google Authenticator
- Supported algorithms:
  - TOTP (Time-based One-time Passwords) as specified in [RFC 6238](https://tools.ietf.org/html/rfc6238)
  - HOTP (HMAC-based One-time Passwords) as specified in [RFC 4226](https://tools.ietf.org/html/rfc4226)

## Backups:

To keep your account information as secure as possible andOTP only stores it in
encrypted data files. A part of the encryption key used for that is stored in the
Android KeyStore system. The advantage of this approach is that the key is kept
separate from the apps data and, as a bonus, can be backed by hardware cryptography
(if your device supports this).

However, due to that separation, backups with 3rd-party apps like Titanium Backup can not
be used with andOTP. Such apps only backup the encrypted data files and not the encryption
key, which renders them useless.

**Please only use the internal backup functions provided by andOTP to backup your accounts!**
**Everything else WILL result in data loss.**

### Opening the backups on your PC:

- [OpenPGP](https://openpgp.org/): OpenPGP can be used to easily decrypt the **OpenPGP-encrypted backups** on your PC.
- [WebDecrypt](https://flocke.shadowice.org/andOTP/decrypt/): JavaScript-based decryption of the **new password-protected backup format** in the browser ([source code](https://github.com/andOTP/WebDecrypt)).
- [andOTP-decrypt](https://github.com/asmw/andOTP-decrypt): Python script written by @asmw to decrypt the **old and new password-protected backup format** on your PC.
- [mac2fa](https://github.com/lorenzo2897/mac2fa): Electron app for macOS that lives in your system tray and generates OTPs from an encrypted backup file.
- [go-andotp](https://github.com/grijul/go-andotp): CLI Program written in go to encrypt/decrypt andOTP files on your PC. Decrypted files can be encrypted and imported back to andOTP.

### Automatic backups:

- BroadcastReceivers: AndOTP supports a number of broadcasts to perform automated backups, eg. via Tasker. These will get saved to the defined backup directory. **These only work when KeyStore is used as the encryption mechanism**
  - **org.shadowice.flocke.andotp.broadcast.PLAIN_TEXT_BACKUP**: Perform a plain text backup. **WARNING**: This will save your 2FA tokens onto the disk in an unencrypted manner!
  - **org.shadowice.flocke.andotp.broadcast.ENCRYPTED_BACKUP**: Perform an encrypted backup of your 2FA database using the selected password in settings.

## Migration:

Check out [this](https://github.com/andOTP/andOTP/wiki/Migration) wiki page to learn about the different ways to migrate to andOTP from other 2FA apps.

## Downloads:

You can download the latest version of andOTP from the following location:

- [Private.coffee Git](https://git.private.coffee/PrivateCoffee/-/packages/generic/andotp/latest) (Latest builds from the main branch, may be unstable)

This APK is based on the F-Droid version of the original project. The Google Play version also still exists, but only within the artifacts of the CI pipeline.

## Contribute:

- **Bug reports and feature requests**: You can report bugs and request features in the issue tracker on [Private.coffee Git](https://git.private.coffee/PrivateCoffee/andOTP/issues) or [GitHub](https://github.com/PrivateCoffee/andOTP/issues).
- **Requesting thumbnails**: If you are missing a thumbnail you can request it by [opening a thumbnail request](https://git.private.coffee/PrivateCoffee/andOTP/issues/new/choose).
- **Discussion and support**:
  - Matrix channel [#general:private.coffee](https://matrix.pcof.fi/#/#general:private.coffee)

#### Donations:

If you want to show your appreciation for our work with a small donation you can do so using the following links:

- [Donate to Jakob Nixdorf](https://flocke.shadowice.org/donate.html) (Main developer and maintainer of the original project)
- [Donate to Private.coffee](https://private.coffee/membership.html) (Maintainer of this fork)

## Screenshots:

#### Light theme:

[<img width=200 alt="Main Activity" src="https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main//assets/screenshots/main_activity.png">](https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/main_activity.png)
[<img width=200 alt="Settings Activity" src="https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main//assets/screenshots/settings_activity.png">](https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/settings_activity.png)
[<img width=200 alt="Backup Activity" src="https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/backup_activity.png">](https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/backup_activity.png)

#### Dark theme:

[<img width=200 alt="Main Activity" src="https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/main_activity_dark.png">](https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/main_activity_dark.png)
[<img width=200 alt="Settings Activity" src="https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/settings_activity_dark.png">](https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/settings_activity_dark.png)
[<img width=200 alt="Backup Activity" src="https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/backup_activity_dark.png">](https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/backup_activity_dark.png)

#### Black theme:

[<img width=200 alt="Main Activity" src="https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/main_activity_black.png">](https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/main_activity_black.png)
[<img width=200 alt="Settings Activity" src="https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/settings_activity_black.png">](https://git.private.coffee/PrivateCoffee/andOTP/raw/branch/main/assets/screenshots/settings_activity_black.png)

## Acknowledgments:

#### Open-source components used:

- [AboutLibraries](https://github.com/mikepenz/AboutLibraries)
- [Apache Commons Codec](https://commons.apache.org/proper/commons-codec/)
- [Floating Action Button Speed Dial](https://github.com/leinardi/FloatingActionButtonSpeedDial)
- [material-intro](https://github.com/heinrichreimer/material-intro)
- [MaterialProgressBar](https://github.com/DreaminginCodeZH/MaterialProgressBar)
- [OpenPGP API library](https://github.com/open-keychain/openpgp-api)
- [ZXing Android Embedded](https://github.com/journeyapps/zxing-android-embedded)
- [Droid Sans Mono Zeromod](https://github.com/AlbertoDorado/droid-sans-mono-zeromod)

#### Code examples used:

- [Android-ItemTouchHelper-Demo](https://github.com/iPaulPro/Android-ItemTouchHelper-Demo/tree/master/app/src/main/java/co/paulburke/android/itemtouchhelperdemo/helper)
- [Code Parts from Google's Android Samples](https://android.googlesource.com/platform/development/+/master/samples/Vault/src/com/example/android/vault)
- [LetterBitmap](https://stackoverflow.com/questions/23122088/colored-boxed-with-letters-a-la-gmail)
- [DimensionConverter](https://stackoverflow.com/questions/8343971/how-to-parse-a-dimension-string-and-convert-it-to-a-dimension-value)
- [NumberPickerPreference](https://github.com/Alobar/AndroidPreferenceTest/tree/master/alobar-preference)

#### Previously used open-source components:

- [FABsMenu](https://github.com/jahirfiquitiva/FABsMenu)
- [LicensesDialog](https://github.com/PSDev/LicensesDialog)
- [VNTNumberPickerPreference](https://github.com/vanniktech/VNTNumberPickerPreference)
- [Expandable Layout](https://github.com/AAkira/ExpandableLayout)

#### Previously used code examples:

- [FloatingActionMenuAndroid](https://github.com/pmahsky/FloatingActionMenuAndroid)

## License:

```
MIT License

Copyright (C) 2025 Private.coffee Team
Copyright (C) 2017-2020 Jakob Nixdorf <andotp@shadowice.org>
Copyright (C) 2015 Bruno Bierbaumer

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in the
Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR
PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE
OR OTHER DEALINGS IN THE SOFTWARE.
```
