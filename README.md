# Pixel Experience

- Sync

        repo init -u https://github.com/ikey4u/pe-manifest -b ten --repo-url https://mirrors.tuna.tsinghua.edu.cn/git/git-repo/
        repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags

    Or you could using a script:

        #! /bin/zsh

        curdir="$(cd "$(dirname "$0")"; pwd -P)"
        cd "$curdir"

        source $HOME/.zshrc

        echo "[$(date)] Start sync lineage ..."
        pyenv local 3.7.5
        repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
        while [[ $? != 0 ]]; do
            echo "[+]  sync failed, try again ..."
            sleep 3
            repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
        done

- Build

        . build/envsetup.sh
        lunch aosp_$device-userdebug
        mka bacon -jX

