# Records

One entry per climate data record in the EUMETSAT Climate Services CDR menu (version 3), with the Data Store title
as the heading. Example filenames are observed examples, not current results. "Unconfirmed" marks values the menu
itself was unsure of.

## Polar-orbiting (LEO)

### AMSR Global Sea Ice Concentration Interim Climate Data Record - Multimission

- Data Store ID: `EO:EUM:DAT:1064`
- Measures: AMSR Global Sea Ice Concentration.
- Sensor and platform: AMSR3, AMSR2 (JAXA); GCOM-W or GOSAT-GW. Orbit: LEO. Level: L3/L4.
- Period: 2021-01-01 to present. Coverage: global. Spatial resolution: 25 km x 25 km. Time step: Daily per hemisphere (unconfirmed).
- Contents: Sea ice concentration [ice_conc] for northern hemisphere [nh] or southern hemisphere [sh] in near-real time [NR/ icdrft/osi-438-a] or non time critical [NT/ icdr/ osi-438].
- Variables to read: `ice_conc`.
- Example filename: `ice_conc_sh_ease2-250_icdrft-v3p0-amsr_202609181200.nc`.
- Note: Shown as Multimission CDR but GCOM-W and GOSAT-GW data are delivered individually on Data Store. OSI SAF page says monthly composites exist, but the Data Store and metadata give twice-daily data.

### AMSU-B Microwave Humidity Sounder Climate Data Record Release 1 - NOAA

- Data Store ID: `EO:EUM:DAT:0303`
- Measures: Microwave humidity sounder brightness temperatures.
- Sensor and platform: AMSU-B; NOAA-15, 16, 17. Orbit: LEO. Level: L1C.
- Period: 1999-01-01 to 2014-06-06. Coverage: global. Spatial resolution: ~16 km at nadir. Time step: Per orbit (~101 min).
- Contents: Top-of-atmosphere (toa) brightness temperatures (BT) for channels 16-20 in Kelvin (K).
- Variables to read: `Ch16_BT`, `Ch17_BT`, `Ch18_BT`, `Ch19_BT`, `Ch20_BT`.
- Example filename: `FIDUCEO_FCDR_L1C_AMSUB_NOAA16_20140605230851_20140606005045_EASY_v4.1_fv2.0.1.nc`.

### ASCAT Level 1 SZF Climate Data Record Release 2 - Metop

- Data Store ID: `EO:EUM:CM:METOP:ASCSZFR02`
- Measures: Scatterometer backscatter (sigma0), full resolution (SZF).
- Sensor and platform: ASCAT; Metop-A. Orbit: LEO. Level: L1B.
- Period: 2007-01-01 to 2014-04-01. Coverage: global. Spatial resolution: Full resolution (~25 x 34 km footprints). Time step: Per orbit (~105 min).
- Contents: Normalised radar cross section / backscatter coefficient (sigma0), incidence angle [INC_ANGLE_FULL], azimuth angle [AZI_ANGLE_FULL].
- Variables to read: `SIGMA0_FULL`, `INC_ANGLE_FULL`, `AZI_ANGLE_FULL`.
- Example filename: `ASCA_SZF_1B_M02_20140331235400Z_20140401013900Z_R_O_20140528192238Z_0200.nat`.
- Note: EPS native format (not netCDF).

### ASCAT Level 1 SZO Climate Data Record Release 2 - Metop

- Data Store ID: `EO:EUM:CM:METOP:ASCSZOR02`
- Measures: Scatterometer backscatter (sigma0) triplets on 25 km swath grid (SZO).
- Sensor and platform: ASCAT; Metop-A. Orbit: LEO. Level: L1B.
- Period: 2007-01-01 to 2014-04-01. Coverage: global. Spatial resolution: 25 km swath grid. Time step: Per orbit (~105 min).
- Contents: Sigma0 triplet (fore/mid/aft beams) [SIGMA0_TRIP], Kp noise estimate [KP], incidence angles [INC_ANGLE_TRIP], azimuth angles [AZI_ANGLE_TRIP].
- Variables to read: `SIGMA0_TRIP`, `KP`, `INC_ANGLE_TRIP`, `AZI_ANGLE_TRIP`.
- Example filename: `ASCA_SZO_1B_M02_20140331235400Z_20140401013856Z_R_O_20140528192253Z_0200.nat`.
- Note: EPS native format (not netCDF).

### ASCAT Level 1 SZR Climate Data Record Release 2 - Metop

- Data Store ID: `EO:EUM:CM:METOP:ASCSZRR02`
- Measures: Scatterometer backscatter (sigma0) triplets on 12.5 km swath grid (SZR).
- Sensor and platform: ASCAT; Metop-A. Orbit: LEO. Level: L1B.
- Period: 2007-01-01 to 2014-04-01. Coverage: global. Spatial resolution: 12.5 km swath grid. Time step: Per orbit (~105 min).
- Contents: Sigma0 triplet (fore/mid/aft beams) [SIGMA0_TRIP], Kp noise estimate [KP], incidence angles [INC_ANGLE_TRIP], azimuth angles [AZI_ANGLE_TRIP].
- Variables to read: `SIGMA0_TRIP`, `KP`, `INC_ANGLE_TRIP`, `AZI_ANGLE_TRIP`.
- Example filename: `ASCA_SZR_1B_M02_20140331235400Z_20140401013858Z_R_O_20140528192253Z_0200.nat`.
- Note: EPS native format (not netCDF).

### ATMS Level 1C Climate Data Record Release 1 - NPP

- Data Store ID: `EO:EUM:DAT:0345`
- Measures: Microwave temperature/humidity sounder brightness temperatures.
- Sensor and platform: ATMS; Suomi-NPP. Orbit: LEO. Level: L1C.
- Period: 2011-12-10 to 2018-12-31. Coverage: global. Spatial resolution: ~16 km (183 GHz) to ~75 km (23/31 GHz) at nadir. Time step: Per orbit (~101 min).
- Contents: Brightness temperature of SNPP [btemps], 22 channels.
- Variables to read: `btemps`.
- Example filename: `C3S_FCDR_L1C_ATMS_SNPP_20181231221642_20181231235808_V1.1_Release1.nc`.

### AVHRR Global (dual) Atmospheric Motion Vectors Climate Data Record Release 1 - Metop-A/B and -B/A

- Data Store ID: `EO:EUM:DAT:0151`
- Measures: Atmospheric Motion Vectors (tropospheric winds), global, Metop-A/B tandem.
- Sensor and platform: AVHRR; Metop-A and B. Orbit: LEO. Level: L2.
- Period: 2013-04-24 to 2017-12-31. Coverage: global. Spatial resolution: Point vectors. Time step: Daily files.
- Contents: Wind speed, direction and height of tracked cloud features.
- Variables to read: not listed in the menu (EPS native format).
- Example filename: `AVHR_AMV_2D_M01_20171231191303Z_20171231191603Z_R_O_20181111145311Z_0100`.
- Note: EPS native format (not netCDF).

### AVHRR Polar Atmospheric Motion Vectors Climate Data Record Release 2 - Metop-A and -B

- Data Store ID: `EO:EUM:DAT:0152`
- Measures: Polar Atmospheric Motion Vectors (tropospheric winds poleward of 45°).
- Sensor and platform: AVHRR; Metop-A and B. Orbit: LEO. Level: L2.
- Period: 2007-03-01 to 2017-12-31. Coverage: Polar >45°N/S. Spatial resolution: Point vectors. Time step: Every ~100 min.
- Contents: Wind speed, direction and height of tracked cloud features.
- Variables to read: not listed in the menu (EPS native format).
- Example filename: `AVHR_AMV_02_M01_20171231233403Z_20171231233703Z_R_O_20181129080104Z_0200`.
- Note: EPS native format (not netCDF). Metop-B only from 24/04/2013.

### CLARA-A3: CM SAF cLoud, Albedo and surface RAdiation dataset from AVHRR data - Edition 3

- Data Store ID: `EO:EUM:DAT:0874`
- Measures: CLARA-A3 cLoud, Albedo, surface Radiation.
- Sensor and platform: AVHRR; Metop, TIROS, NOAA. Orbit: LEO. Level: L3.
- Period: 1979-01-01 to present. Coverage: global and polar. Spatial resolution: 0.25° x 0.25°. Time step: Daily, monthly 5-day.
- Contents: Fractional cloud cover [CFC], Cloud phase [CPH], Cloud top parameters [CTO], TOA Outgoing Longwave Radiation [OLR] and Reflected Solar Flux [RSF], Surface albedo [SAL], Surface Radiation products [SDL, SIS, SNL, SNS, SRB],.
- Variables to read: `blue_sky_albedo_all_mean` for surface albedo (`SAL`). For the other products, inspect one file first.
- Example filename: `SALmm20260801000000319AVPOSI1GL.nc`.
- Packaging: Not bundled: one netCDF file per product and time step. Filename = product code + time-step code: `dm` daily mean, `mm` monthly mean, `pm` 5-day (pentad) mean for albedo. Filter on both, for example `SALmm*`.
- Note: CMA, CTX, LWP, IWP, CPP, CWP, JCH listed in the metadata but were not found on the Data Store when the menu was compiled.

### AVHRR GAC Atmospheric Motion Vectors Climate Data Record Release 2 - Multimission - Polar

- Data Store ID: `EO:EUM:DAT:0558`
- Measures: Polar Atmospheric Motion Vectors (IR 10.8 µm).
- Sensor and platform: AVHRR (GAC); TIROS-N, NOAA-6 to -19, Metop-A and B. Orbit: LEO. Level: L2.
- Period: 1979-01-01 to 2019-09-01. Coverage: Polar. Spatial resolution: Point vectors. Time step: Per orbit (~100 min).
- Contents: Wind speed, direction, u/v components and height of tracked cloud / water vapour features.
- Variables to read: `wind_speed`, `wind_from_direction`, `eastward_wind`, `northward_wind`, `wind_pressure`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,IR+ATMOSPHERE+AMV,NOAA15+AVHRR_C_EUMP_20190901002203Z_20190901013403Z_polar_r_gac_l2_0200.nc`.

### Polar Multi-Sensor Aerosol Optical Properties Climate Data Record Release 1 - Metop-A and -B

- Data Store ID: `EO:EUM:DAT:0579`
- Measures: Aerosol optical depth (550 nm) and aerosol type.
- Sensor and platform: GOME-2, AVHRR, IASI; Metop-A and B. Orbit: LEO. Level: L2.
- Period: 2007-07-10 to 2019-08-31. Coverage: global. Spatial resolution: ~10 x 40 km. Time step: Per orbit (~100 min).
- Contents: Aerosol optical depth at 550 nm; aerosol class (fine, dust, volcanic ash, biomass).
- Variables to read: `aerosol_optical_depth`, `aerosol_class`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,SOUNDING+SATELLITE,METOPB+GOME_C_EUMP_20190831221956_36076_eps_r_pmap_l2_0100.nc`.
- Note: Variables are inside netCDF groups (Data/MeasurementData/ObservationData/Aerosol).

### IASI All Sky Temperature and Humidity Profiles - Climate Data Record Release 1.1 - Metop-A and -B

- Data Store ID: `EO:EUM:DAT:0576`
- Measures: All Sky Temperature and Humidity Profiles.
- Sensor and platform: IASI; Metop-A and B. Orbit: LEO. Level: L2.
- Period: 2007-07-10 to 2023-12-31. Coverage: global. Spatial resolution: IASI pixel (unconfirmed). Time step: Twice daily.
- Contents: T (temperature), W (water vapour), pressure_levels (for T & W), Ts (surface T), Ps (surface P), CloudFraction, WC (cloud water content), LandFraction. Quality flags (Q) for variables as well as FLG_IASIBAD, FLG_MHSBAD, FLG_AMSUBAD, FLG_INITIA, OmC.
- Variables to read: `T`, `W`, `Ts`, `Ps`, `pressure_levels`, `CloudFraction`, `WC`, `LandFraction`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,HYPERSPECT+SOUNDING,METOPB+PW3+IASI_C_EUMP_20231231230856Z_20240101005055Z_eps_r_l2_0101.nc`.

### IASI Level 1C Climate Data Record Release 2 - Metop-A and -B

- Data Store ID: `EO:EUM:DAT:0590`
- Measures: Infrared radiance spectra (8461 channels, 645-2760 cm-1).
- Sensor and platform: IASI; Metop-A and B. Orbit: LEO. Level: L1C.
- Period: 2007-07-10 to 2019-10-01. Coverage: global. Spatial resolution: 12 km at nadir. Time step: Per orbit (~102 min).
- Contents: Calibrated infrared radiance spectra.
- Variables to read: `GS1cSpect`.
- Example filename: `IASI_xxx_1C_M02_20190930222655Z_20191001000854Z_R_O_20240610091504Z_0200.nat`.
- Note: EPS native format (not netCDF). ~1.4 GB per file.

### IASI Carbon Monoxide Profiles FORLI-CO Climate Data Record Release 1 - Metop-A and -B

- Data Store ID: `EO:EUM:DAT:0959`
- Measures: Carbon Monoxide FORLI-CO.
- Sensor and platform: IASI; Metop-A and B. Orbit: LEO. Level: L2.
- Period: 2007-07-10 to 2023-12-31. Coverage: global. Spatial resolution: IASI pixel (unconfirmed). Time step: Twice daily.
- Contents: scaling factors on a-priori [co_x_co], a-priori partial columns [co_cp_co_a], air partial columns [co_cp_air], partial layer heights [forli_layer_heights_co].
- Variables to read: `co_x_co`, `co_cp_co_a`, `co_cp_air`, `forli_layer_heights_co`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,HYPERSPECT+SOUNDING,METOPB+CO+IASI_C_EUMP_20231231230856Z_20240101005055Z_eps_r_l2_0100.nc`.

### IASI SO2 Climate Data Record Release 1 - Metop-A and -B

- Data Store ID: `EO:EUM:DAT:0960`
- Measures: Sulphur Dioxide (SO2).
- Sensor and platform: IASI; Metop-A and B. Orbit: LEO. Level: L2.
- Period: 2007-07-10 to 2023-12-31. Coverage: global. Spatial resolution: IASI pixel (unconfirmed). Time step: Twice daily.
- Contents: so2_col (interpolated column product).
- Variables to read: `so2_col`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,HYPERSPECT+SOUNDING,METOPB+SO2+IASI_C_EUMP_20231231230856Z_20240101005055Z_eps_r_l2_0100.nc`.

### IASI Ozone (O3) Climate Data Record (CDR) Release 1 - Metop-A and -B

- Data Store ID: `EO:EUM:DAT:1027`
- Measures: Ozone (O3).
- Sensor and platform: IASI; Metop-A and B. Orbit: LEO. Level: L2.
- Period: 2007-07-10 to 2023-12-31. Coverage: global. Spatial resolution: IASI pixel (unconfirmed). Time step: Twice daily.
- Contents: Scaling factors on the a-priori [o3_x_o3], a-priori partial columns[o3_cp_o3_a].
- Variables to read: `o3_x_o3`, `o3_cp_o3_a`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,HYPERSPECT+SOUNDING,METOPB+O3+IASI_C_EUMP_20231231230856Z_20240101005055Z_eps_r_l2_0100.nc`.

### MHS Microwave Humidity Sounder Climate Data Record Release 1 - Metop and NOAA

- Data Store ID: `EO:EUM:DAT:0305`
- Measures: Microwave humidity sounder brightness temperatures.
- Sensor and platform: MHS; NOAA-18, 19, Metop-A and B. Orbit: LEO. Level: L1C.
- Period: 2005-08-30 to 2018-01-01. Coverage: global. Spatial resolution: ~16 km at nadir. Time step: Per orbit (~101 min).
- Contents: Top-of-atmosphere (toa) brightness temperatures (BT) for channels 1-5 in Kelvin (K).
- Variables to read: `Ch1_BT`, `Ch2_BT`, `Ch3_BT`, `Ch4_BT`, `Ch5_BT`.
- Example filename: `FIDUCEO_FCDR_L1C_MHS_METOPB_20171231222436_20180101000556_EASY_v4.1_fv2.0.1.nc`.
- Note: Superseded for Metop by Release 2 (EO:EUM:DAT:0344).

### MHS Microwave Humidity Sounder Climate Data Record Release 2 - Metop-A and -B

- Data Store ID: `EO:EUM:DAT:0344`
- Measures: Microwave humidity sounder brightness temperatures.
- Sensor and platform: MHS; Metop-A and B. Orbit: LEO. Level: L1C.
- Period: 2006-10-31 to 2018-12-31. Coverage: global. Spatial resolution: ~16 km at nadir. Time step: Per orbit (~101 min).
- Contents: Brightness temperature of Metop-A/B [btemps], 5 channels.
- Variables to read: `btemps`.
- Example filename: `C3S_FCDR_L1C_MHS_METOPA_20181231220445_20181231234605_V1.1_Release2.nc`.

### MWHS-1 Level 1C Climate Data Record Release 1

- Data Store ID: `EO:EUM:DAT:0348`
- Measures: Microwave humidity sounder brightness temperatures.
- Sensor and platform: MWHS-1; FengYun-3A and 3B. Orbit: LEO. Level: L1C.
- Period: 2008-07-01 to 2018-12-31. Coverage: global. Spatial resolution: ~15 km at nadir. Time step: Per orbit (~101 min).
- Contents: Brightness temperature of FY-3A/3B [btemps], 5 channels.
- Variables to read: `btemps`.
- Example filename: `C3S_FCDR_L1C_MWHS_FY3B_20181231204812_20181231222955_V1.1_Release1.nc`.

### MWHS-2 Level 1C Climate Data Record Release 1

- Data Store ID: `EO:EUM:DAT:0349`
- Measures: Microwave humidity sounder brightness temperatures.
- Sensor and platform: MWHS-2; FengYun-3C. Orbit: LEO. Level: L1C.
- Period: 2013-09-30 to 2018-12-31. Coverage: global. Spatial resolution: ~15 km (183/150 GHz), ~30 km (118 GHz) at nadir. Time step: Per orbit (~101 min).
- Contents: Brightness temperature of FY-3C [btemps], 15 channels.
- Variables to read: `btemps`.
- Example filename: `C3S_FCDR_L1C_MWHS2_FY3C_20181231181716_20181231195858_V1.1_Release1.nc`.

### SSM/T-2 Microwave Humidity Sounder Climate Data Record Release 2 - DMSP

- Data Store ID: `EO:EUM:DAT:0343`
- Measures: Microwave humidity sounder brightness temperatures.
- Sensor and platform: SSM/T-2; DMSP F11, F12, F14, F15. Orbit: LEO. Level: L1C.
- Period: 1994-07-05 to 2005-01-10. Coverage: global. Spatial resolution: ~48 km at nadir. Time step: Per orbit (~102 min).
- Contents: Brightness temperature of DMSP [tb], 5 channels, plus cloud flag [cloud_flag].
- Variables to read: `tb`, `cloud_flag`.
- Example filename: `C3S_FCDR_L1C_SSMT2_F14_20050110183418_20050110193958_R02.0.nc`.

### Global Sea Ice Concentration Interim Climate Data Record Release 3 - DMSP

- Data Store ID: `EO:EUM:DAT:0645`
- Measures: DMSP Global Sea Ice Concentration.
- Sensor and platform: SSMIS; DMSP. Orbit: LEO. Level: L3/L4.
- Period: 2023-09-03 to present. Coverage: global. Spatial resolution: 26 km x 25 km. Time step: Daily per hemisphere.
- Contents: Sea ice concentration [ice_conc] for northern hemisphere [nh] or southern hemisphere [sh] in non time critical [NT/ icdr/ osi-430-a].
- Variables to read: `ice_conc`.
- Example filename: `ice_conc_sh_ease2-250_icdr-v3p0_202509291200.nc`.

## Polar and geostationary (LEO + GEO)

### GIRAFE v1: CM SAF Global Interpolated RAinFall Estimation version 1

- Data Store ID: `EO:EUM:DAT:0921`
- Measures: GIRAFE Global Interpolated RAinFall.
- Sensor and platform: GOES Imager, VISSR, JAMI, MVIRI, AHI, MTSAT-2 Imager, ABI, SEVIRI, FCI; MSG, MTG, GOES, Himawari, MFG. Orbit: LEO + GEO. Level: L3.
- Period: 2002-01-01 to present. Coverage: global. Spatial resolution: 1° x 1°. Time step: Daily, monthly.
- Contents: precipitation [PRE].
- Variables to read: `precipitation`.
- Example filename: `PREmm20260801000000120IMPGSI1GL.nc`.
- Packaging: One file per time step. Filename codes: `PREdm` daily, `PREmm` monthly.

## Geostationary (GEO)

### GSA Level 2 Climate Data Record Release 2 - MFG - 57 degree

- Data Store ID: `EO:EUM:DAT:0301`
- Measures: Land surface albedo (black-sky and white-sky), Indian Ocean 57°E.
- Sensor and platform: MVIRI; Meteosat-7. Orbit: GEO. Level: L2.
- Period: 2006-12-07 to 2017-03-31. Coverage: Meteosat disk at 57°E. Spatial resolution: ~2.5 km. Time step: 10-day.
- Contents: Black-sky albedo [DHR30] and white-sky albedo [BHRiso], 0-1.
- Variables to read: `DHR30`, `BHRiso`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,SURFACE+SAT,MET07+MVIRI+GSA_C_EUMS_20170322000000_20170331235959_1_OR_FES_E0570_0200.nc`.
- Note: Data Store footprint is misplaced (west of Greenwich), so area searches may miss files.

### GSA Level 2 Climate Data Record Release 2 - MFG - 63 degree

- Data Store ID: `EO:EUM:DAT:0302`
- Measures: Land surface albedo (black-sky and white-sky), Indian Ocean 63°E.
- Sensor and platform: MVIRI; Meteosat-5. Orbit: GEO. Level: L2.
- Period: 1998-07-10 to 2007-04-10. Coverage: Meteosat disk at 63°E. Spatial resolution: ~2.5 km. Time step: 10-day.
- Contents: Black-sky albedo [DHR30] and white-sky albedo [BHRiso], 0-1.
- Variables to read: `DHR30`, `BHRiso`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,SURFACE+SAT,MET05+MVIRI+GSA_C_EUMS_20070401000000_20070410235959_1_OR_FES_E0630_0200.nc`.
- Note: Data Store footprint is misplaced (west of Greenwich), so area searches may miss files.

### MVIRI Level 1.5 Climate Data Record Release 2 - MFG - 0 degree

- Data Store ID: `EO:EUM:DAT:0880`
- Measures: Visible, infrared and water vapour imagery, 0° disk.
- Sensor and platform: MVIRI; Meteosat-2 to -7. Orbit: GEO. Level: L1.5.
- Period: 1982-08-11 to 2006-07-19. Coverage: Meteosat 0° disk. Spatial resolution: VIS 2.5 km, IR/WV 5 km. Time step: 30-minute.
- Contents: Top-of-atmosphere visible reflectance; infrared and water vapour counts.
- Variables to read: `toa_bidirectional_reflectance_vis`, `count_ir`, `count_wv`.
- Example filename: `MVIRI_FCDR-EASY_L15_MET7-E0000_200607182330_200607190000_0200.nc`.
- Note: No lat/lon in files.

### MVIRI Level 1.5 Climate Data Record Release 2 - MFG - 57 degree

- Data Store ID: `EO:EUM:DAT:0881`
- Measures: Visible, infrared and water vapour imagery, Indian Ocean 57°E.
- Sensor and platform: MVIRI; Meteosat-7. Orbit: GEO. Level: L1.5.
- Period: 2006-11-01 to 2017-04-04. Coverage: Meteosat disk at 57°E. Spatial resolution: VIS 2.5 km, IR/WV 5 km. Time step: 30-minute.
- Contents: Top-of-atmosphere visible reflectance; infrared and water vapour counts.
- Variables to read: `toa_bidirectional_reflectance_vis`, `count_ir`, `count_wv`.
- Example filename: `MVIRI_FCDR-EASY_L15_MET7-E5700_201704032330_201704040000_0200.nc`.
- Note: No lat/lon in files.

### MVIRI Level 1.5 Climate Data Record Release 2 - MFG - 63 degree

- Data Store ID: `EO:EUM:DAT:0882`
- Measures: Visible, infrared and water vapour imagery, Indian Ocean 63°E.
- Sensor and platform: MVIRI; Meteosat-5. Orbit: GEO. Level: L1.5.
- Period: 1998-07-01 to 2006-10-31. Coverage: Meteosat disk at 63°E. Spatial resolution: VIS 2.5 km, IR/WV 5 km. Time step: 30-minute.
- Contents: Top-of-atmosphere visible reflectance; infrared and water vapour counts.
- Variables to read: `toa_bidirectional_reflectance_vis`, `count_ir`, `count_wv`.
- Example filename: `MVIRI_FCDR-EASY_L15_MET5-E6300_200610302330_200610310000_0200.nc`.
- Note: No lat/lon in files.

### Atmospheric Motion Vectors Climate Data Record Release 1 - MFG - Indian Ocean 57 degrees E

- Data Store ID: `EO:EUM:DAT:0894`
- Measures: Atmospheric Motion Vectors (winds from WV 6.2 µm and IR 10.8 µm), Indian Ocean 57°E.
- Sensor and platform: MVIRI; Meteosat-7. Orbit: GEO. Level: L2.
- Period: 2006-11-28 to 2017-04-01. Coverage: Meteosat disk at 57°E. Spatial resolution: Point vectors. Time step: 2-hourly.
- Contents: Wind speed, direction, u/v components and height of tracked cloud / water vapour features.
- Variables to read: `speed`, `dir`, `u`, `v`, `height`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,IR+ATMOSPHERE+AMV,MET7+MVIRI_C_EUMS_20170331220000Z_20170401000000Z_1_OR_FES_E0570_0100.nc`.

### Atmospheric Motion Vectors Climate Data Record Release 1 - MFG - Indian Ocean 63 degrees E

- Data Store ID: `EO:EUM:DAT:0895`
- Measures: Atmospheric Motion Vectors (winds from WV 6.2 µm and IR 10.8 µm), Indian Ocean 63°E.
- Sensor and platform: MVIRI; Meteosat-5. Orbit: GEO. Level: L2.
- Period: 1998-07-01 to 2007-04-16. Coverage: Meteosat disk at 63°E. Spatial resolution: Point vectors. Time step: 2-hourly.
- Contents: Wind speed, direction, u/v components and height of tracked cloud / water vapour features.
- Variables to read: `speed`, `dir`, `u`, `v`, `height`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,IR+ATMOSPHERE+AMV,MET5+MVIRI_C_EUMS_20070416040000Z_20070416060000Z_1_OR_FES_E0630_0100.nc`.
- Note: Data Store footprint is misplaced (west of Greenwich), so area searches may miss files.

### Surface Radiation Data Set - Heliosat (SARAH) - Edition 3

- Data Store ID: `EO:EUM:DAT:0863`
- Measures: SARAH Surface Radiation DataSet Heliosat.
- Sensor and platform: MVIRI + SEVIRI; MFG and MSG. Orbit: GEO. Level: L3.
- Period: 1983-01-01 to present. Coverage: Meteosat 0° disk. Spatial resolution: 0.05° x 0.05°. Time step: 30-min instant, daily, monthly.
- Contents: Daylight (DAL), Sunshine Duration (SDU), Surface incoming direct radiation (SID), Photosynthetic Active Radiation (PAR), Direct Normal Irradiance (DNI), Surface incoming shortwave radiation (SIS), Effective cloud albedo (CAL). Daily and monthly DAL, DNI, PAR, SID, SIS also contain a clear-sky measurement (C).
- Variables to read: the product code, plus a clear-sky variable with a `C` suffix in daily and monthly DAL, DNI, PAR, SID and SIS files: for example `DNI` and `DNIC`.
- Example filename: `DNImm2026080100000042310001I1MA.nc`.
- Packaging: Not bundled: one netCDF file per product and time step (30-minute, daily, monthly). Filename = product code + time-step code: `in` 30-minute instantaneous, `dm` daily mean, `mm` monthly mean; sunshine duration uses `ds` and `ms`. Filter on both, for example `SISmm*`.

### GSA Level 2 Climate Data Record Release 2 - MFG and MSG - 0 degree

- Data Store ID: `EO:EUM:DAT:0300`
- Measures: Land surface albedo (black-sky and white-sky).
- Sensor and platform: MVIRI, SEVIRI; Meteosat-2 to -7 (MFG), Meteosat-8 to -10 (MSG). Orbit: GEO. Level: L2.
- Period: 1982-02-10 to 2017-12-31. Coverage: Meteosat 0° disk. Spatial resolution: 3 km. Time step: 10-day.
- Contents: Black-sky albedo [DHR30] and white-sky albedo [BHRiso], 0-1.
- Variables to read: `DHR30`, `BHRiso`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,SURFACE+SAT,MET10+SEVIRI+GSA_C_EUMG_20171227000000_20171231235959_1_OR_FES_E0000_0200.nc`.

### Atmospheric Motion Vectors Climate Data Record Release 2 - MFG and MSG - 0 degree

- Data Store ID: `EO:EUM:DAT:0405`
- Measures: Atmospheric Motion Vectors (winds from WV 6.2 µm and IR 10.8 µm), 0° disk.
- Sensor and platform: MVIRI, SEVIRI; Meteosat-2 to -7 (MFG), Meteosat-8 to -11 (MSG). Orbit: GEO. Level: L2.
- Period: 1981-09-03 to 2019-09-01. Coverage: Meteosat 0° disk. Spatial resolution: Point vectors. Time step: 2-hourly (MFG), hourly (MSG).
- Contents: Wind speed, direction, u/v components and height of tracked cloud / water vapour features.
- Variables to read: `speed`, `dir`, `u`, `v`, `height`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,IR+ATMOSPHERE+AMV,MSG4+SEVIRI_C_EUMG_20190831230000Z_20190901000000Z_1_OR_FES_E0000_0200.nc`.

### Optimal Cloud Analysis Climate Data Record Release 1 - MSG - 0 degree

- Data Store ID: `EO:EUM:DAT:0617`
- Measures: OCA Optimal Cloud Analysis (CLAAS).
- Sensor and platform: SEVIRI; MSG1-4. Orbit: GEO. Level: L2.
- Period: 2004-01-19 to 2019-08-31. Coverage: not global. Spatial resolution: 4 km x 3 km. Time step: 15-minute.
- Contents: scene_classification, cloud_probability, cloud_top_pressure, cloud_particle_effective_radius.
- Variables to read: `scene_classification`, `cloud_particle_effective_radius`, `cloud_top_pressure`, `cloud_probability`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,OCA+MSG4+SEVIRI_C_EUMG_20190831234500_1_OR_FES_E0000_0100.nc`.

### Atmospheric Motion Vectors Climate Data Record Release 1 - MSG - Indian Ocean 41.5 degrees E

- Data Store ID: `EO:EUM:DAT:0896`
- Measures: Atmospheric Motion Vectors (winds from WV 6.2 µm and IR 10.8 µm), Indian Ocean 41.5°E.
- Sensor and platform: SEVIRI; Meteosat-8 (MSG1). Orbit: GEO. Level: L2.
- Period: 2017-02-01 to 2019-09-01. Coverage: No (Meteosat disk at 41.5°E). Spatial resolution: Point vectors. Time step: Hourly.
- Contents: Wind speed, direction, u/v components and height of tracked cloud / water vapour features.
- Variables to read: `speed`, `dir`, `u`, `v`, `height`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,IR+ATMOSPHERE+AMV,MSG1+SEVIRI_C_EUMG_20190831230000Z_20190901000000Z_1_OR_FES_E0415_0100.nc`, `W_XX-EUMETSAT-Darmstadt,WV+ATMOSPHERE+AMV,MSG1+SEVIRI_C_EUMG_20190831230000Z_20190901000000Z_1_OR_FES_E0415_0100.nc`.
- Note: Separate IR and WV files.

### OCA Atmospheric Motion Vectors Climate Data Record Release 1 - MSG - 0 degree

- Data Store ID: `EO:EUM:DAT:1082`
- Measures: OCA Atmospheric Motion Vectors.
- Sensor and platform: SEVIRI; MSG1-4. Orbit: GEO. Level: L2.
- Period: 2004-01-19 to 2019-08-31. Coverage: not global. Spatial resolution: Ground resolution 3 km at sub-satellite point. Time step: Hourly.
- Contents: Wind vectors AMV speed (ms-1), direction (degree), and height (pressure units hPa).
- Variables to read: `speed`, `dir`, `height`, `u`, `v`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,WV73+ATMOSPHERE+AMV+OCA,MSG4+SEVIRI_C_EUMG_20190831230000Z_20190901000000Z_1_OR_FES_E0000_0100.nc`.
- Packaging: BUNDLED. Downloaded product contains 3 nc files for channels IR108, WV62, WV73.

### SEVIRI Rapid Scan High Rate Level 1.5 Image Data Climate Data Record Release 1 - MSG

- Data Store ID: `EO:EUM:DAT:0962`
- Measures: Visible and infrared imagery, rapid scan (all 12 channels).
- Sensor and platform: SEVIRI Rapid Scan; Meteosat-8, -9, -10 (MSG1-3). Orbit: GEO. Level: L1.5.
- Period: 2008-05-06 to 2021-09-22. Coverage: Europe and North Africa, ~13-81°N. Spatial resolution: 3 km (HRV 1 km). Time step: 5-minute.
- Contents: Raw counts for all 12 SEVIRI channels, with recalibration coefficients.
- Variables to read: `counts_vis006 ... counts_ir134`, `counts_hrv`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,VIS+IR+HRV+IMAGERY,MSG3+SEVIRI_C_EUMG_20210922235916_0100.nc`.
- Note: Counts, not radiances. Recalibration only until 04/2020.

### SEVIRI Rapid Scan Atmospheric Motion Vectors Climate Data Record Release 1 - MSG

- Data Store ID: `EO:EUM:DAT:1083`
- Measures: Atmospheric Motion Vectors.
- Sensor and platform: SEVIRI Rapid Scan; Meteosat-8, -9, -10 (MSG1-3). Orbit: GEO. Level: L2.
- Period: 2008-05-06 to 2020-04-03. Coverage: Europe and North Africa, ~13-81°N. Spatial resolution: 3 km x 3 km. Time step: 5-minute.
- Contents: wind_speed, wind_from_direction, air_pressure (height of AMV), air_temperature, u (zonal), v (meridional wind component)..
- Variables to read: `wind_speed`, `wind_from_direction`, `air_pressure`, `air_temperature`, `u`, `v`.
- Example filename: `W_XX-EUMETSAT-Darmstadt,VIS_IR_WV+ATMOSPHERE+HRW,MSG3+SEVIRI_C_EUMG_20200403T234500Z_20200403T235500Z_1_OR_RSS_E0950_0100.nc`.
- Packaging: Internal variables are nested under channel groups: wind_ir108, wind_wv062, wind_wv073, wind_hrvis, wind_vis06.

