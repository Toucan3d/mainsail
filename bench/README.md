# Toucan3D test bench page

`public/bench/index.html` is a standalone dashboard for the Toucan3D Klipper
test bench. It mirrors the KlipperScreen bench layout and lists the test
data files. It talks to Moonraker over the same-origin websocket, so it needs
no API key or CORS setting.

A Mainsail build from this branch serves it at `/bench/`. On the bench Pi it
currently runs next to an upstream Mainsail v2.19.0 release:

- the page lives in `~/toucan-bench-ui/index.html`
- `~/mainsail/bench` is a symlink to `~/toucan-bench-ui`
- `bench` is listed under `persistent_files` in `[update_manager mainsail]`
  of `moonraker.conf`, so Mainsail updates keep it
- `navi.json` from this folder is placed in `~/printer_data/config/.theme/`
  and adds the "Testbench" entry to the Mainsail sidebar
