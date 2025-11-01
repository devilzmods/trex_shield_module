ZMK Module with studio support and bluetooth for the lovely T-Rex keyboard by Sylivan Kenobi:
https://github.com/SylivanKenobi/t-rex

My personal build uses the nice! Nano v2, so that's what i can guarantee it to work with.

To include the module add the marked lines (>) to your zmk-config/config/west.yml:

    manifest:
      defaults:
        revision: v0.3
      remotes:
        - name: zmkfirmware
          url-base: https://github.com/zmkfirmware
    >    - name: trex_shield_module
    >      url-base: https://github.com/devilzmods/
        # Additional modules containing boards/shields/custom code can be listed here as well
        # See https://docs.zephyrproject.org/3.2.0/develop/west/manifest.html#projects
      projects:
        - name: zmk
          remote: zmkfirmware
          import: app/west.yml
    >    - name: trex_shield_module
    >      remote: trex_shield_module
    >      revision: main
      self:
        path: config

zmk-config/build.yml should look like this:

    ---
    include:
      - board: nice_nano_v2 #your controller of choice
        shield: t_rex
        snippet: studio-rpc-usb-uart #zmk-usb-logging 
        cmake-args: -DCONFIG_ZMK_STUDIO=y
        artifact-name: t_rex_with_studio
