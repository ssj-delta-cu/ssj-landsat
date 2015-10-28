#! /usr/bin/make -f
SHELL:=/bin/bash

gdal_merge:=gdal_merge.py

dates:=2014285 2014301 2014333 2014349 2014365 \
2015016 2015032 2015048 2015064 2015080 \
2015096 2015112 2015128 2015144 2015160 \
2015176 2015192 2015208 2015224 2015240 \
2015256 2015272

scenes:=044033 044034
xmls:=$(foreach s,${scenes},$(patsubst %,LC8${s}%LGN00.xml,${dates}))
# This is the UTM bounding box for Delta region
# with b as (select st_transform(boundary,26910) as b from bbox) select format('%s %s %s %s',(st_xmin(b)-120)::integer,(st_ymax(b)+120)::integer,(st_xmax(b)+120)::integer,(st_ymin(b)-120)::integer) as ul_lr from b;
ul_lr:=596898 4276385 656760 4162602

bands:=sr_band1 sr_band2 sr_band3 sr_band4 sr_band5 sr_band6 sr_band7
more:=cfmask_conf cloud cfmask

tifs:=$(patsubst %,%/ref.tif,${dates})

.PHONY:tifs
tifs:${tifs}

${tifs}:%/ref.tif:
		[[ -f LC8044033$*LGN00.xml ]] || tar -xzf data/LC8044033$*-SC*.tar.gz
		[[ -f LC8044033$*LGN00.xml ]] || tar -xzf data/LC8044033$*-SC*.tar.gz
		[[ -d $* ]] || mkdir $*
		for b in ${bands}; do\
				${gdal_merge} -o $*/$$b.tif -ul_lr ${ul_lr} -n -9999 LC804403[34]$*LGN00_$$b.tif; \
				list+=" $*/$$b.tif";\
		done;\
		${gdal_merge} -o $*/sr_cloud.tif -ul_lr ${ul_lr} -n 0 LC804403[34]$*LGN00_sr_cloud.tif;\
		${gdal_merge} -o $*/cfmask.tif -ul_lr ${ul_lr} -n 255 LC804403[34]$*LGN00_cfmask.tif;\
		${gdal_merge} -o $*/cfmask_conf.tif -ul_lr ${ul_lr} -n 0 LC804403[34]$*LGN00_cfmask_conf.tif;\
		${gdal_merge} -separate -o $@ $$list $*/sr_cloud.tif;\
		${gdal_merge} -separate -o $*_cf.tif $*/cfmask.tif $*/cfmask_conf.tif;\
		rm -f LC804403[34]$*LGN00*;\
		rm -f $$list
