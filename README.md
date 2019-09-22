
# RAY

## Clone & Run

```bash
git clone git@github.com:craft-de-jet/app.git ray && cd ray
git submodule update --init --recursive -- services/dashboard-ui/
docker container rm dash-ui dashKdmStyles dashKdmComponents
DSBD_WEB_PORT=3000 DSBD_WEB_FS_PORT=35729 DSBD_API_PORT=5000 DSBD_API_DBG_PORT=50001 docker-compose -f docker-compose.build.yml up --build
DSBD_WEB_PORT=3000 DSBD_WEB_FS_PORT=35729 DSBD_API_PORT=5000 DSBD_API_DBG_PORT=50001 docker-compose -f docker-compose.yml up --build
```
