# Installing Adobe Photoshop CC on case-sensitive drives (Mac OS X)

Well, everybody knows that Adobe are a **[censored]** company.
Their products are the defacto standard for image/video editing and designing, but their codebase really suck. No excuses.

The problem addressed here is that Creative Studio™ refuses to install on a case-sensitive drive on Mac OS X.
And it doesn't just refuse to install on a case-sensitive drive, but it also requires to install on your *boot* drive as well! Srsly?

Well, there's a solution. I've just stumbled upon [this](https://bitbucket.org/lokkju/adobe_case_sensitive_volumes), and I'm really anxious to share it.
I've forked the code to update it for Photoshop CC.

## Prerequisites

1.  `Xcode`

    You can install it from [AppStore](https://itunes.apple.com/app/xcode/id497799835).
2.  Command Line Tools for Xcode.

    You can install it from Xcode's `Preferences` -> `Downloads`.

## A step-by-step installation instructions

1.  Create a `.sparsebundle` pseudo-image to install CS6:

    ``` bash
    mkdir -p ~/Stuff/Adobe
    cd ~/Stuff/Adobe
    hdiutil create -size 15g -type SPARSEBUNDLE -nospotlight -volname 'Adobe Photoshop SparseBundle' -fs 'Journaled HFS+' ~/Stuff/Adobe/Adobe_Photoshop_SparseBundle.sparsebundle
    ```

2.  Mount the newly created image and create a `/Adobe` directory inside

    ``` bash
    open ~/Stuff/Adobe/Adobe_Photoshop_SparseBundle.sparsebundle
    mkdir -p /Volumes/Adobe\ Photoshop\ SparseBundle/Adobe
    ```
    
3. Symlink the install directory to the pseudo-image

    `ln -s /Volumes/Adobe\ Photoshop\ SparseBundle/Adobe /Applications/Adobe`

4.  Get the hack, compile it, and run it
    ``` bash
    cd ~/Stuff/Adobe
    git clone git://github.com/nacholibre/photoshop_cc_case_sensitive_install_mac_osx.git
    cd photoshop_cc_case_sensitive_install_mac_osx
    make
    sudo make run
    ```

5.  The installer will open, if not, click on the Icon in the dock and install Photoshop.

6. That's it, you are done!

## Thanks

[lokkju](https://bitbucket.org/lokkju), for writing [that awesome article and code](https://bitbucket.org/lokkju/adobe_case_sensitive_volumes) to start from
