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
        mka bacon -jX

