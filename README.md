# Pixel Experience

- Sync

        repo init -u https://github.com/ikey4u/pe-manifest -b ten --repo-url https://mirrors.tuna.tsinghua.edu.cn/git/git-repo/
        repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags

    Or you may use a script

        curl -LO https://raw.githubusercontent.com/ikey4u/pe-manifest/ten/syncme

    Then change the script to fit your situation and run.

- Build

        . build/envsetup.sh
        lunch aosp_$device-userdebug
        time mka bacon -jX

- Building for `Redmi Note 7 Pro`

    - Overview

        Full building steps

            . build/envsetup.sh
            lunch aosp_violet-userdebug
            time mka bacon -j$(nproc --all)

    - Details

        lunch will call the following python script

            roomserivce.py violet

        roomserivce will do the following stuffs

        1. query from github

            The requested url is

                https://api.github.com/search/repositories?q=violet+user:PixelExperience-Devices+in:name+fork:true

            it will find `device_xiaomi_violet` and clone it to local `device/xiaomi/violet`.

        2. Adding dependencies and fetching

            Then it will add `device/xiaomi/violet/aosp.dependencies` into
            `.repo/local_manifests/pixel.xml` and fetch these dependencies.

    - Appendix

        I use zsh and pyenv to do the building. If you encounter the following errors:

            pyenv: python3.6: command not found

        This is an issue of pyenv, you may solve it by

            pyenv local 2.7.15 3.6.5

        Google's repo tool unable to write log (`vendor/aosp/tools/changelog.sh`), I do not know why, ignored.

            Got an error, terminating the pool: ValueError: I/O operation on closed file
