# Batch Connect - OSC ANSYS Workbench

![GitHub Release](https://img.shields.io/github/release/osc/bc_osc_ansys_workbench.svg)
![GitHub License](https://img.shields.io/github/license/osc/bc_osc_ansys_workbench.svg)

A VNCSim app designed for OSC OnDemand that launches ANSYS Workbench within an
Oakley batch job. It runs in a heavily customized desktop/environment so that
it works in OSC's supercomputer environment.

## Install

1. Git clone this app in the desired location and go into the directory:

  ```sh
  git clone <repo> bc_osc_ansys_workbench

  cd bc_osc_ansys_workbench
  ```

2. Checkout the version of the app you want to deploy:

  ```sh
  git checkout <tag>
  ```

2. This app requires the
   [bc_fvwm_assets](https://github.com/OSC/bc_fvwm_assets) Bower asset, so we
   will need a local copy of Bower:

   ```sh
   npm install bower
   ```

3. Install the Bower asset:

  ```sh
  node_modules/.bin/bower install
  ```

## Update

1. Fetch the updated code:

  ```sh
  git fetch
  ```

2. Checkout the desired tag:

  ```sh
  git checkout <tag>
  ```

3. Update the Bower assets:

  ```sh
  node_modules/.bin/bower update --force
  ```

## Specification

### ROOT

All assets in this package look for dependencies in the specified `$ROOT`
directory. This should be set to correspond to the included `template/`
directory.

An example running the `xstartup` script included in this package:

```sh
# Path where you installed this project
BC_OSC_ANSYS_WORKBENCH_DIR="/path/to/bc_osc_ansys_workbench/template"

# Run the `xstartup` script with proper `$ROOT` set
ROOT="${BC_OSC_ANSYS_WORKBENCH_DIR}" ${BC_OSC_ANSYS_WORKBENCH_DIR}/xstartup
```

### ANSYS_MODULE

This environment variable describes the specific ANSYS version to load. This
also assumes module support through the
[Lmod](https://www.tacc.utexas.edu/research-development/tacc-projects/lmod)
package manager is installed on the running compute node as well as the
requested module in `$ANSYS_MODULE`.

### GPU_OFF

*Optional*

If this environment variables is set, then it will *attempt* to run the various
ANSYS workbench packages in software rendering mode. Not all packages currently
support this, so bugs may arise for the user as they use the workbench.

If this is unset (default), then it will use
[VirtualGL](http://www.virtualgl.org/) giving the ANSYS Workbench full 3D
hardware acceleration support inside the VNC session. Note that an `Xorg`
server must be running on the compute node with a GPU for this to be supported.

## Contributing

1. Fork it ( https://github.com/OSC/bc_osc_ansys_workbench/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
