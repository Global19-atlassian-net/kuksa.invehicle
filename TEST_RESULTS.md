/*
* ******************************************************************************
* Copyright (c) 2019 Expleo Germany.
*
* All rights reserved. This program and the accompanying materials
* are made available under the terms of the Eclipse Public License v2.0
* which accompanies this distribution, and is available at
* https://www.eclipse.org/org/documents/epl-2.0/index.php
*
*  Contributors:
*      * Expleo Germany
* *****************************************************************************
*/

# Test-Results (March - June/July 2019)

## Developer Stories
| Step:                            | Operation:                                       | Errors:                                                                                                                                                                                                                                                                                                 |
|----------------------------------|--------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Building image (docker)          | `./build.sh <architecture>`                        | - <span style="color:salmon">Does not work with the cloud-mechanic (arguments interpreted wrong)</span> <br>https://github.com/eclipse/kuksa.apps/issues/8                                                                                                                                                 |
| Building image (Tape-Archive)    | `docker save <ID> > <tarname>.tar`                 | <span style="color:green">None</span>                                                                                                                                                                                                                                                                   |
| Upload Image (Appstore/ HawkBit) | `python3 app-publisher <ID> <app-config>.yaml -n`  | - <span style="color:salmon">publisher NEEDS already loaded docker image</span><br>  - <span style="color:salmon">publisher generates `docker-container.json` but it's ignored by the installer</span> <br> - <span style="color:green">Image is uploaded to Appstore + Hawkbit for Download</span><br> |
| Re-Upload Image                  | `python3 app-publisher <ID>  <app-config>.yaml -r` | - <span style="color:salmon">won’t update, if the config-file changed. Even an increased version-number prevents the reupload.</span> <br>https://github.com/eclipse/kuksa.apps/issues/16                                                                                                                  |                                                                  |

## User Stories

| Step:                | Operation:                                                                                        | Errors:                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| starting Appmanager  | 1. start with docker (inkl. HONO) <br> 2. start with docker (no HONO) <br> 3. start as systemservice (no Hono)<br> 4. start as systemservice (+ Hono)          | 1. <span style="color:salmon">HONO-parameters are misinterpreted, which bricks the App-Manager</span> <br>https://github.com/eclipse/kuksa.invehicle/issues/57 <br> 2. <span style="color:green">None</span> <br>  3. <span style="color:green">None</span> <span style="color:salmon"><br>https://github.com/eclipse/kuksa.invehicle/issues/9</span> <br>combined issue:<br> https://github.com/eclipse/kuksa.invehicle/issues/60  |
| buying an App        | click `buy` in appstore                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                     |
| downloading App      | click `download` in appstore                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                     |
| installing App       | happens automatically after download                                                              | <span style="color:salmon">`.tar` is downloaded, but not automatically loaded/installed</span>  <br>  Pratheek/Sebastian : newer version uses .tar.bz2                                                                                                                                                                                                                                                                                                                   |
| running app (auto)   |                                                                                                   | <span style="color:salmon">despite an existing `docker-container.json`  the app wont be executed after downloading it </span>                                                                                                                                                                                                                                                                                       |
| running app (manual) |       `docker run -e <param1> -e ... <ID>`                                                                                            | <span style="color:green">None</span>                                                                                                                                                                                                                                                                                                                                                                               |
| uninstalling App     | clicking `uninstall` in appstore <br> https://kuksa-appstore.appstacle.appstaclecloud.org:8443/#!login | <span style="color:salmon">Won't be uninstalled from device. Change is detected, but nothing will change on the device. References to installed apps (online and offline) won't be changed/deleted                                                                                                                                                                                                                     |

## Test Stories

| Step:                    | Operation:                     | Errors:                                          |
|--------------------------|--------------------------------|--------------------------------------------------|
| download App (HawkBit)   | `./foreverChecker`             | <span style="color:green">None</span>                                             |
| download App (App-Store) | `./foreverChecker`             | <span style="color:green">None                                       </span>                                             |      |
| uninstall App (HawkBit)  | Drag `uninstall` onto device   | <span style="color:salmon">Won't uninstall but triggers process</span>                                             |             |
| uninstall App            | click `uninstall` in App-Store | <span style="color:salmon">Change is detected, but App won't be uninstalled</span>                                             | |

# References
- [AGL Storage issue (invehicle:64)](https://github.com/eclipse/kuksa.invehicle/issues/64)
- [App-manager infinte Download-loop (invehicle:63)](https://github.com/eclipse/kuksa.invehicle/issues/63)
- [How to start App-manager (invehicle:60)](https://github.com/eclipse/kuksa.invehicle/issues/60)
- [Runing App-Manager without  docker fails (invehicle:59)](https://github.com/eclipse/kuksa.invehicle/issues/59)
- [App-Manager misinterprets HONO-Prams (invehicle:57)](https://github.com/eclipse/kuksa.invehicle/issues/57)


- [App-Publisher never re-publishes (apps:16)](https://github.com/eclipse/kuksa.apps/issues/16)
- [Invalid architecture in build-script (apps:9)](https://github.com/eclipse/kuksa.apps/issues/9)
- [Building Cloud-Mechanic fails (apps:8)](https://github.com/eclipse/kuksa.apps/issues/8)

- [App-Publisher Borked naming-convention (apps:15)](https://github.com/eclipse/kuksa.apps/issues/15)
- [App-Publisher no docker-standards (apps:14)](https://github.com/eclipse/kuksa.apps/issues/14)

