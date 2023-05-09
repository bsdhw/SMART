HDD/SSD Reliability Test
------------------------

This is a project to estimate reliability of HDD/SSD drives by
the analysis of SMART data collected by BSD users at https://bsd-hardware.info. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe/blob/master/INSTALL.BSD.md) tool:

    hw-probe -all -upload

Total drives: 13809.

Contents
--------

1. [ About          ](#about)
2. [ HDD by Model   ](#hdd-by-model)
3. [ HDD by Vendor  ](#hdd-by-vendor)
4. [ SSD by Model   ](#ssd-by-model)
5. [ SSD by Vendor  ](#ssd-by-vendor)
6. [ NVMe by Model  ](#nvme-by-model)
7. [ NVMe by Vendor ](#nvme-by-vendor)

About
-----

The structure of the reports directory is the following:

    {KIND OF DRIVE}/{VENDOR}/{MODEL PREFIX}/{MODEL}/{DRIVE ID}

    ( e.g. HDD/Seagate/ST1000/ST1000LM035-1RK172/3F1554E2F97E )

Based on SMART data we determine most reliable drive models and vendors by the
following formula:

    MTBF = Power_On_Hours / ( 1 + Number_Of_Important_Errors ) / ( 365*24 )

    ( i.e. MTBF = "Years before/between errors" )

Number_Of_Important_Errors - number of important errors that can indicate a drive failure:

* Current_Pending_Sector
* ECC_Uncorr_Error_Count
* End-to-End_Error
* Offline_Uncorrectable
* Reallocated_Event_Count
* Reallocated_Sector_Ct
* Reported_Uncorrect
* Soft_Read_Error_Rate
* Spin_Retry_Count
* Total_Pending_Sectors
* Unc_Soft_Read_Err_Rate

One can estimate reliability of a hard drive (i.e. probability that the unit will work
for some time T without failure) by:

    Reliability(T) = exp(-T/MTBF)

The list of important SMART attributes is taken from recent studies of Google [1],
Backblaze [2] and Acronis [3]. If an attribute exceeds the value of 1000 then it's
counted as '1000 + log10(X - 999)'.

The list of tracked attributes and MTBF calculation method can be discussed. Please
suggest your ideas in "issues".

You can perform your own analysis of collected reports if needed.

* [1] Google, "Failure Trends in a Large Disk Drive Population" (https://research.google.com/archive/disk_failures.pdf)
* [2] Backblaze, "Hard Drive SMART Stats" (https://www.backblaze.com/blog/hard-drive-smart-stats/)
* [3] Acronis, "Acronis Drive Monitor: Disk Health Calculation" (https://kb.acronis.com/content/9264)

HDD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

See top 1000 of tested HDD models in the [Top1000_HDD.md](/Top1000_HDD.md).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| WDC       | WD1600JD-00GBB0    | 160 GB | 4       | 5313  | 4     | 11.14  |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 4       | 3874  | 0     | 10.61  |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 3       | 3833  | 0     | 10.50  |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 2       | 3820  | 0     | 10.47  |
| Hitachi   | HDS725050KLA360    | 500 GB | 4       | 3436  | 0     | 9.41   |
| WDC       | WD5002ABYS-50B1B1  | 500 GB | 2       | 3336  | 0     | 9.14   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 3       | 3099  | 0     | 8.49   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 6       | 3085  | 0     | 8.45   |
| Seagate   | ST3808110AS        | 80 GB  | 2       | 2844  | 0     | 7.79   |
| Seagate   | ST3500630NS        | 500 GB | 5       | 2830  | 0     | 7.75   |
| Hitachi   | HUA7250SBSUN500G   | 500 GB | 2       | 2785  | 0     | 7.63   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 4       | 2778  | 0     | 7.61   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 4       | 2729  | 0     | 7.48   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 5       | 2687  | 0     | 7.36   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 2       | 2628  | 0     | 7.20   |
| Hitachi   | HDT725025VLA380    | 250 GB | 2       | 2611  | 0     | 7.15   |
| Seagate   | ST3320413AS        | 320 GB | 2       | 2575  | 0     | 7.06   |
| Hitachi   | HUA721050KLA330    | 500 GB | 2       | 3842  | 1     | 7.02   |
| Samsung   | HD502IJ            | 500 GB | 2       | 2696  | 1     | 6.93   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 3       | 3373  | 11    | 6.91   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 4       | 2488  | 0     | 6.82   |
| Seagate   | ST32000641AS       | 2 TB   | 5       | 2443  | 0     | 6.69   |
| HP        | GB0250EAFYK        | 250 GB | 3       | 3054  | 1     | 6.61   |
| HGST      | HUS724020ALA640    | 2 TB   | 10      | 2400  | 0     | 6.58   |
| WDC       | WD1600AAJS-00Z4A0  | 160 GB | 2       | 2386  | 0     | 6.54   |
| Seagate   | ST380011A          | 80 GB  | 2       | 2353  | 0     | 6.45   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 2       | 2343  | 0     | 6.42   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 9       | 2333  | 0     | 6.39   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 9       | 2520  | 1     | 6.36   |
| WDC       | WD1003FBYX-23 0... | 1 TB   | 2       | 2317  | 0     | 6.35   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 2       | 2316  | 0     | 6.35   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 2       | 2315  | 0     | 6.35   |
| WDC       | WD5002ABYS-18B1B0  | 500 GB | 3       | 2886  | 3     | 6.35   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 6       | 2580  | 2     | 6.26   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 3       | 2236  | 0     | 6.13   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 6       | 2447  | 1     | 6.07   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 2168  | 0     | 5.94   |
| HGST      | HDN724040ALE640    | 4 TB   | 40      | 2315  | 71    | 5.85   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 27      | 2494  | 1     | 5.84   |
| HP        | GB0500EAFYL        | 500 GB | 4       | 2079  | 0     | 5.70   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 9       | 2078  | 0     | 5.69   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 2       | 2076  | 0     | 5.69   |
| Hitachi   | HDS5C4040ALE630    | 4 TB   | 21      | 2076  | 0     | 5.69   |
| WDC       | WD3200BEKT-08PVMT1 | 320 GB | 5       | 2075  | 0     | 5.69   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 4       | 2069  | 0     | 5.67   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 2       | 2045  | 0     | 5.60   |
| HGST      | HDN724030ALE640    | 3 TB   | 9       | 2037  | 0     | 5.58   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 6       | 3011  | 2     | 5.57   |
| Hitachi   | HDS728080PLA380    | 82 GB  | 2       | 2026  | 0     | 5.55   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 2       | 2009  | 0     | 5.51   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 2       | 2004  | 0     | 5.49   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 7       | 1993  | 0     | 5.46   |
| Hitachi   | HTE543232A7A384    | 320 GB | 3       | 1975  | 0     | 5.41   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 7       | 2136  | 145   | 5.37   |
| Seagate   | ST32000645NS       | 2 TB   | 2       | 1938  | 0     | 5.31   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 14      | 2581  | 55    | 5.25   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 2       | 1916  | 0     | 5.25   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 18      | 2020  | 2     | 5.23   |
| HP        | MB1000GCEEK        | 1 TB   | 3       | 1896  | 0     | 5.20   |
| HGST      | HTE721010A9E630    | 1 TB   | 3       | 1849  | 0     | 5.07   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 10      | 1993  | 2     | 5.01   |
| WDC       | WD2500AAKX-753CA1  | 250 GB | 3       | 1828  | 0     | 5.01   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 2       | 1816  | 0     | 4.98   |
| Seagate   | ST4000NC000-1FR168 | 4 TB   | 2       | 1810  | 0     | 4.96   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 14      | 1892  | 145   | 4.92   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 3       | 1792  | 0     | 4.91   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 2       | 3527  | 3     | 4.88   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 15      | 1999  | 83    | 4.84   |
| Toshiba   | MG03ACA200         | 2 TB   | 6       | 1760  | 0     | 4.82   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 4       | 1752  | 0     | 4.80   |
| Seagate   | ST6000DX000-1H217Z | 6 TB   | 2       | 1714  | 0     | 4.70   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 5       | 1795  | 1     | 4.67   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 15      | 1951  | 135   | 4.64   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 33      | 1736  | 32    | 4.61   |
| HPE       | MB4000GCWLV        | 4 TB   | 9       | 1662  | 0     | 4.55   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 4       | 2240  | 2     | 4.52   |
| Toshiba   | MG04ACA400E        | 4 TB   | 2       | 1635  | 0     | 4.48   |
| Seagate   | ST3300831AS        | 304 GB | 2       | 2192  | 1059  | 4.37   |
| Hitachi   | HDT725032VLA360    | 320 GB | 3       | 2689  | 2     | 4.36   |
| Hitachi   | HUA721075KLA330    | 752 GB | 2       | 1592  | 0     | 4.36   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 2       | 1587  | 0     | 4.35   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 4       | 1574  | 0     | 4.31   |
| Samsung   | HD204UI            | 2 TB   | 20      | 2071  | 7     | 4.30   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 8       | 1557  | 0     | 4.27   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 3       | 3550  | 4     | 4.25   |
| Seagate   | ST3500414CS        | 500 GB | 7       | 1551  | 5     | 4.25   |
| WDC       | WD20NMVW-11EDZS2   | 2 TB   | 2       | 1545  | 0     | 4.23   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 3       | 1544  | 0     | 4.23   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 2       | 2615  | 545   | 4.22   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 5       | 1520  | 0     | 4.17   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 2       | 1517  | 0     | 4.16   |
| Maxtor    | 6L080J4            | 80 GB  | 3       | 2093  | 2     | 4.15   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 2       | 1504  | 0     | 4.12   |
| HP        | MB1000GCWCV        | 1 TB   | 7       | 2011  | 4     | 4.09   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 4       | 1560  | 1     | 4.05   |
| WDC       | WD2500JS-75NCB2    | 250 GB | 4       | 1473  | 0     | 4.04   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 9       | 2227  | 229   | 4.03   |
| WDC       | WD2000FYYX         | 2 TB   | 4       | 1466  | 0     | 4.02   |
| Hitachi   | HDE721064SLA360    | 640 GB | 2       | 2248  | 6     | 4.00   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 2       | 1460  | 0     | 4.00   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 4       | 1909  | 1     | 3.97   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 2       | 1450  | 0     | 3.97   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 40      | 1813  | 1     | 3.97   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 2       | 1449  | 0     | 3.97   |
| Hitachi   | HDP725050GLA360    | 500 GB | 4       | 1735  | 10    | 3.97   |
| Seagate   | ST3250312AS        | 250 GB | 7       | 1442  | 0     | 3.95   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 4       | 2692  | 3     | 3.94   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 3       | 1529  | 3     | 3.92   |
| Hitachi   | HDS721075KLA330    | 752 GB | 9       | 1767  | 1     | 3.90   |
| Samsung   | HD502HI            | 500 GB | 2       | 1402  | 0     | 3.84   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 4       | 1386  | 0     | 3.80   |
| Toshiba   | MG04ACA100N        | 1 TB   | 2       | 1383  | 0     | 3.79   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 14      | 2309  | 158   | 3.78   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 5       | 1373  | 0     | 3.76   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 15      | 1531  | 1     | 3.76   |
| HP        | VB0250EAVER        | 250 GB | 3       | 2037  | 2     | 3.76   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 5       | 1352  | 0     | 3.71   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 4       | 1797  | 28    | 3.71   |
| Samsung   | HD322HJ            | 320 GB | 10      | 1548  | 61    | 3.69   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 11      | 1331  | 0     | 3.65   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 36      | 1725  | 54    | 3.64   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 3       | 1317  | 0     | 3.61   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 70      | 1535  | 1     | 3.58   |
| WDC       | WD2503ABYZ-011FA0  | 256 GB | 2       | 1306  | 0     | 3.58   |
| Toshiba   | MK2561GSYB         | 250 GB | 2       | 1306  | 0     | 3.58   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 13      | 1385  | 1     | 3.58   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 4       | 1301  | 0     | 3.57   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 7       | 1301  | 0     | 3.57   |
| Seagate   | ST33000651AS       | 3 TB   | 2       | 1296  | 0     | 3.55   |
| Samsung   | HD154UI            | 1.5 TB | 8       | 2606  | 276   | 3.52   |
| HGST      | HDN726040ALE614    | 4 TB   | 15      | 1509  | 2     | 3.51   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 3       | 1278  | 0     | 3.50   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 2       | 1268  | 0     | 3.48   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 2       | 1266  | 0     | 3.47   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 6       | 1467  | 2     | 3.46   |
| Samsung   | HD161GJ            | 160 GB | 3       | 1263  | 0     | 3.46   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 2       | 1260  | 0     | 3.45   |
| Seagate   | ST9500620NS        | 500 GB | 3       | 2190  | 25    | 3.45   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 9       | 1245  | 0     | 3.41   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 3       | 1243  | 0     | 3.41   |
| HGST      | HUS726040ALN610    | 4 TB   | 2       | 1239  | 0     | 3.40   |
| Samsung   | HD103SJ            | 1 TB   | 9       | 1786  | 227   | 3.38   |
| WDC       | WD3200AAKX-001CA0  | 320 GB | 3       | 2227  | 5     | 3.38   |
| Toshiba   | DT01ACA200         | 2 TB   | 12      | 1375  | 95    | 3.37   |
| HP        | FB160C4081         | 160 GB | 3       | 3197  | 3     | 3.32   |
| Maxtor    | 6V080E0            | 80 GB  | 2       | 1262  | 1     | 3.32   |
| WDC       | WD1600BEVT-22A23T0 | 160 GB | 2       | 1205  | 0     | 3.30   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 8       | 1506  | 2     | 3.30   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 2       | 2395  | 260   | 3.29   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 10      | 1199  | 0     | 3.29   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 3       | 1629  | 24    | 3.25   |
| HGST      | HDN728080ALE604    | 8 TB   | 7       | 1182  | 0     | 3.24   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 4       | 1181  | 0     | 3.24   |
| HGST      | HTE725032A7E630    | 320 GB | 6       | 1452  | 10    | 3.21   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 7       | 1476  | 13    | 3.20   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 3       | 1167  | 0     | 3.20   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 6       | 1679  | 2     | 3.20   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 6       | 1273  | 1     | 3.19   |
| WDC       | WD1001FALS-403AA0  | 1 TB   | 3       | 1495  | 264   | 3.19   |
| WDC       | WD5000AACS-00ZUB0  | 500 GB | 2       | 1155  | 0     | 3.16   |
| WDC       | WD3000BLFS-60YBU2  | 304 GB | 2       | 1399  | 1     | 3.13   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 6       | 2271  | 46    | 3.13   |
| Seagate   | ST3320613AS        | 320 GB | 2       | 1995  | 11    | 3.10   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 2       | 1415  | 4     | 3.09   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 4       | 1116  | 0     | 3.06   |
| Hitachi   | HTS545016B9A300    | 160 GB | 2       | 1116  | 0     | 3.06   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 2       | 2202  | 3     | 3.05   |
| WDC       | WD2005FBYZ-01YCBB1 | 2 TB   | 2       | 1111  | 0     | 3.05   |
| WDC       | WD3200BEKT-00KA9T0 | 320 GB | 2       | 1109  | 0     | 3.04   |
| WDC       | WD4002FYYZ-01B7CB0 | 4 TB   | 3       | 1082  | 0     | 2.97   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 3       | 1308  | 1     | 2.95   |
| HGST      | HUS724040ALA640    | 4 TB   | 5       | 1058  | 0     | 2.90   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 6       | 1467  | 1     | 2.90   |
| Seagate   | ST3500413AS        | 500 GB | 18      | 1433  | 280   | 2.89   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 3       | 1273  | 1     | 2.88   |
| Samsung   | HD502HJ            | 500 GB | 9       | 1589  | 1     | 2.86   |
| WDC       | WD3200AAKS-75L9A0  | 320 GB | 2       | 1472  | 2     | 2.86   |
| Toshiba   | MQ01ABD100H        | 1 TB   | 2       | 1041  | 0     | 2.85   |
| Seagate   | ST3160318AS        | 160 GB | 11      | 1326  | 49    | 2.84   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 30      | 1265  | 202   | 2.83   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 4       | 1055  | 6     | 2.83   |
| Toshiba   | MC04ACA400E        | 4 TB   | 2       | 1023  | 0     | 2.80   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 4       | 1880  | 326   | 2.80   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 11      | 1090  | 184   | 2.80   |
| Samsung   | HD103UJ            | 1 TB   | 9       | 1787  | 27    | 2.79   |
| ExcelStor | J8160              | 164 GB | 2       | 1015  | 0     | 2.78   |
| WDC       | WD1600AAJS-60Z0A0  | 160 GB | 2       | 1445  | 803   | 2.77   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 3       | 1293  | 3     | 2.76   |
| HPE       | MB4000GVYZK        | 4 TB   | 8       | 1005  | 0     | 2.76   |
| Seagate   | ST380815AS         | 80 GB  | 12      | 1447  | 461   | 2.75   |
| Toshiba   | HDWE150            | 5 TB   | 6       | 1186  | 5     | 2.73   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 5       | 2630  | 386   | 2.73   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 2       | 990   | 0     | 2.71   |
| Samsung   | HM500JI            | 500 GB | 4       | 1251  | 53    | 2.71   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 2       | 986   | 0     | 2.70   |
| Seagate   | ST9160411AS        | 160 GB | 2       | 1221  | 3     | 2.68   |
| WDC       | WD1600AAJS-40H3A0  | 160 GB | 2       | 975   | 0     | 2.67   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 3       | 974   | 0     | 2.67   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 2       | 972   | 0     | 2.66   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 1449  | 1     | 2.65   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 19      | 1086  | 62    | 2.65   |
| Samsung   | HD501LJ            | 500 GB | 12      | 2110  | 256   | 2.64   |
| WDC       | WD5000BEVT-22ZAT0  | 500 GB | 2       | 953   | 0     | 2.61   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 4       | 950   | 0     | 2.60   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 9       | 947   | 0     | 2.59   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 19      | 945   | 0     | 2.59   |
| Seagate   | ST3750528AS        | 752 GB | 3       | 1686  | 45    | 2.57   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 4       | 1234  | 2     | 2.57   |
| Toshiba   | DT01ACA300         | 3 TB   | 15      | 1101  | 69    | 2.57   |
| Seagate   | ST3250318AS        | 250 GB | 11      | 1224  | 82    | 2.56   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 22      | 1000  | 1     | 2.56   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 7       | 1060  | 3     | 2.55   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 10      | 1459  | 233   | 2.53   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 6       | 920   | 0     | 2.52   |
| HGST      | HDN721010ALE604    | 10 TB  | 3       | 916   | 0     | 2.51   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 5       | 1121  | 1     | 2.50   |
| Seagate   | ST3500312CS        | 500 GB | 15      | 1033  | 64    | 2.50   |
| Seagate   | ST1000NM0018-2F... | 1 TB   | 2       | 910   | 0     | 2.49   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 3       | 907   | 0     | 2.49   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 6       | 1575  | 3     | 2.48   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1316  | 6     | 2.47   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 2       | 900   | 0     | 2.47   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 10      | 1096  | 105   | 2.43   |
| Toshiba   | MD04ACA400         | 4 TB   | 4       | 920   | 3     | 2.43   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 3       | 1105  | 400   | 2.42   |
| Seagate   | ST32000542AS       | 2 TB   | 4       | 1291  | 241   | 2.41   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 7       | 1178  | 3     | 2.40   |
| Samsung   | HD753LJ            | 752 GB | 4       | 1723  | 423   | 2.40   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 3       | 1742  | 13    | 2.39   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 5       | 1067  | 2     | 2.39   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 3       | 869   | 0     | 2.38   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 15      | 1207  | 37    | 2.38   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 6       | 1057  | 2     | 2.38   |
| Seagate   | ST1000NM0011       | 1 TB   | 4       | 1690  | 8     | 2.37   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 10      | 861   | 0     | 2.36   |
| Hitachi   | HDP725025GLA380    | 250 GB | 2       | 1109  | 2     | 2.36   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 12      | 859   | 0     | 2.36   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 11      | 856   | 0     | 2.35   |
| Maxtor    | STM3250310AS       | 250 GB | 4       | 927   | 1     | 2.34   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 2       | 1242  | 3     | 2.33   |
| Seagate   | ST91000640NS       | 1 TB   | 2       | 847   | 0     | 2.32   |
| Hitachi   | HDS721050CLA662    | 500 GB | 2       | 844   | 0     | 2.32   |
| Seagate   | ST14000NM0018-2... | 14 TB  | 2       | 840   | 0     | 2.30   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 2       | 837   | 0     | 2.29   |
| Maxtor    | STM3160815AS       | 160 GB | 3       | 1028  | 320   | 2.27   |
| HGST      | HUS726020ALA610    | 2 TB   | 2       | 822   | 0     | 2.25   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 3       | 1049  | 3     | 2.25   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 5       | 818   | 0     | 2.24   |
| WDC       | WD1200BB-00HTA0    | 120 GB | 2       | 1633  | 347   | 2.24   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 7       | 1391  | 3     | 2.23   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 23      | 930   | 4     | 2.23   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 10      | 1363  | 414   | 2.23   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 2       | 810   | 0     | 2.22   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 2       | 810   | 0     | 2.22   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 8       | 810   | 0     | 2.22   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 11      | 809   | 0     | 2.22   |
| Seagate   | ST500DM002-1SB10A  | 500 GB | 6       | 805   | 0     | 2.21   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 3       | 1323  | 33    | 2.21   |
| Toshiba   | MG03ACA100         | 1 TB   | 10      | 803   | 0     | 2.20   |
| Lenovo    | WD2004FBYZ-23YC... | 2 TB   | 4       | 802   | 0     | 2.20   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 2       | 802   | 0     | 2.20   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 2       | 833   | 4     | 2.18   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 30      | 1004  | 46    | 2.17   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 2       | 790   | 0     | 2.17   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 13      | 1091  | 138   | 2.16   |
| Fujitsu   | MHW2120BH          | 120 GB | 3       | 779   | 0     | 2.14   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 2       | 774   | 0     | 2.12   |
| WDC       | WD5000LUCT-63RC2Y0 | 500 GB | 2       | 773   | 0     | 2.12   |
| Hitachi   | HTS727550A9E364    | 500 GB | 5       | 1038  | 233   | 2.11   |
| Hitachi   | HDS721050CLA660    | 500 GB | 6       | 1418  | 338   | 2.11   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 9       | 1667  | 485   | 2.11   |
| Seagate   | ST3320620AS        | 320 GB | 7       | 1418  | 173   | 2.10   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 4       | 866   | 2     | 2.10   |
| Seagate   | ST380817AS         | 80 GB  | 4       | 760   | 0     | 2.08   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 2       | 754   | 0     | 2.07   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 4       | 915   | 93    | 2.05   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 4       | 1199  | 4     | 2.04   |
| Seagate   | ST9250410AS        | 250 GB | 7       | 800   | 34    | 2.03   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 9       | 794   | 1     | 2.03   |
| WDC       | WD5000AAKX-00U6AA0 | 500 GB | 3       | 802   | 1     | 2.02   |
| WDC       | WD1600BEVT-75ZCT2  | 160 GB | 5       | 735   | 0     | 2.01   |
| Seagate   | ST3160812AS        | 160 GB | 5       | 1031  | 261   | 2.00   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 3       | 1665  | 2     | 1.99   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 4       | 726   | 0     | 1.99   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 6       | 803   | 1     | 1.98   |
| Toshiba   | HDWD120            | 2 TB   | 9       | 715   | 2     | 1.95   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 10      | 799   | 1     | 1.95   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 5       | 709   | 0     | 1.94   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 4       | 1016  | 2     | 1.93   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 13      | 1253  | 172   | 1.93   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 6       | 702   | 0     | 1.92   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 4       | 1849  | 4     | 1.92   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 7       | 1458  | 35    | 1.92   |
| Toshiba   | HDWN180            | 8 TB   | 12      | 699   | 0     | 1.92   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 2       | 1368  | 4     | 1.91   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 5       | 696   | 0     | 1.91   |
| Samsung   | HD103SI            | 1 TB   | 5       | 823   | 606   | 1.91   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 5       | 693   | 0     | 1.90   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 7       | 686   | 0     | 1.88   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 15      | 674   | 0     | 1.85   |
| Hitachi   | HTS725032A9A364    | 320 GB | 3       | 1248  | 342   | 1.81   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 4       | 655   | 0     | 1.80   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 3       | 655   | 0     | 1.80   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 8       | 692   | 67    | 1.80   |
| Seagate   | ST380013AS         | 80 GB  | 6       | 1319  | 5     | 1.79   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 3       | 885   | 1     | 1.77   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 11      | 647   | 0     | 1.77   |
| Toshiba   | DT01ACA050         | 500 GB | 27      | 851   | 11    | 1.77   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 80      | 650   | 1     | 1.74   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 14      | 683   | 2     | 1.73   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 23      | 722   | 6     | 1.73   |
| Seagate   | ST3160813AS        | 160 GB | 4       | 839   | 1     | 1.72   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 2       | 623   | 0     | 1.71   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 3       | 622   | 0     | 1.71   |
| Toshiba   | DT01ACA100         | 1 TB   | 42      | 766   | 50    | 1.71   |
| HPE       | MB0500GCEHE        | 500 GB | 6       | 659   | 2     | 1.70   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 77      | 1040  | 180   | 1.69   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 2       | 616   | 0     | 1.69   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 6       | 733   | 1     | 1.69   |
| HGST      | HUS726040ALE610    | 4 TB   | 3       | 1030  | 464   | 1.68   |
| Seagate   | ST3160023AS        | 160 GB | 2       | 1239  | 3     | 1.68   |
| Hitachi   | HTS545025B9A300    | 250 GB | 9       | 667   | 224   | 1.68   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 2       | 611   | 0     | 1.68   |
| Seagate   | ST31000524AS       | 1 TB   | 11      | 1052  | 217   | 1.67   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 37      | 654   | 5     | 1.66   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 4       | 796   | 416   | 1.64   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 2       | 593   | 0     | 1.63   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 2       | 589   | 0     | 1.62   |
| WDC       | WD2500YS-01SHB1    | 256 GB | 2       | 589   | 0     | 1.61   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 6       | 580   | 0     | 1.59   |
| Samsung   | HM250HI            | 250 GB | 6       | 626   | 14    | 1.58   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 2       | 575   | 0     | 1.58   |
| HGST      | HUS726T4TALA6L1    | 4 TB   | 2       | 574   | 0     | 1.57   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 4       | 573   | 0     | 1.57   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 3       | 1376  | 3     | 1.57   |
| Apple     | HDD HTS547550A9... | 500 GB | 3       | 598   | 10    | 1.56   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 12      | 626   | 1     | 1.53   |
| Hitachi   | HDS721050CLA362    | 500 GB | 4       | 615   | 254   | 1.53   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 4       | 556   | 0     | 1.53   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 9       | 555   | 0     | 1.52   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 4       | 545   | 0     | 1.49   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 13      | 542   | 0     | 1.49   |
| Samsung   | HD250HJ            | 250 GB | 2       | 1028  | 1211  | 1.49   |
| Toshiba   | HDWQ140            | 4 TB   | 18      | 541   | 0     | 1.48   |
| Seagate   | ST3000NM0005-1V... | 3 TB   | 3       | 540   | 0     | 1.48   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 10      | 1121  | 6     | 1.48   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 6       | 595   | 2     | 1.48   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 2       | 537   | 0     | 1.47   |
| Seagate   | ST3500418AS        | 500 GB | 30      | 1243  | 118   | 1.47   |
| HGST      | HTE545032A7E380    | 320 GB | 3       | 521   | 0     | 1.43   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 3       | 554   | 1     | 1.43   |
| Seagate   | ST3160815AS        | 160 GB | 12      | 1279  | 92    | 1.43   |
| WDC       | WD10JPVX-00JC3T0   | 1 TB   | 6       | 581   | 2     | 1.42   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 3       | 513   | 0     | 1.41   |
| WDC       | WD3200BPVT-22ZEST0 | 320 GB | 2       | 509   | 0     | 1.40   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 13      | 598   | 75    | 1.39   |
| HGST      | HTS721010A9E630    | 1 TB   | 29      | 591   | 185   | 1.38   |
| Seagate   | ST3750640AS        | 752 GB | 2       | 1505  | 2     | 1.38   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 8       | 1322  | 192   | 1.36   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 10      | 554   | 1     | 1.34   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 2       | 486   | 0     | 1.33   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 2       | 482   | 0     | 1.32   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 9       | 518   | 4     | 1.31   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 12      | 498   | 1     | 1.31   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 8       | 570   | 9     | 1.30   |
| Seagate   | ST500NM0011        | 500 GB | 4       | 1711  | 20    | 1.30   |
| Seagate   | ST6000NE0023-2E... | 6 TB   | 2       | 853   | 4     | 1.30   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 40      | 630   | 3     | 1.29   |
| Apple     | HDD HTS541010A9... | 1 TB   | 3       | 736   | 2     | 1.28   |
| Seagate   | ST3320418AS        | 320 GB | 6       | 929   | 357   | 1.27   |
| Samsung   | HD161HJ            | 160 GB | 7       | 755   | 377   | 1.27   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 9       | 462   | 0     | 1.27   |
| Fujitsu   | MHY2120BH          | 120 GB | 2       | 456   | 0     | 1.25   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 4       | 507   | 2     | 1.24   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 2       | 856   | 68    | 1.22   |
| WDC       | WD80EDAZ-11TA3A0   | 8 TB   | 3       | 576   | 1     | 1.21   |
| Hitachi   | HDT725032VLA380    | 320 GB | 2       | 441   | 0     | 1.21   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 3       | 440   | 0     | 1.21   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 4       | 439   | 0     | 1.20   |
| Seagate   | ST3320820AS        | 320 GB | 3       | 437   | 0     | 1.20   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 12      | 435   | 0     | 1.19   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 2       | 695   | 1     | 1.19   |
| Seagate   | ST2000NE0025-2F... | 2 TB   | 2       | 433   | 0     | 1.19   |
| Hitachi   | HTS541080G9SA00    | 80 GB  | 2       | 565   | 1     | 1.19   |
| HGST      | HTS541010A9E680    | 1 TB   | 16      | 515   | 258   | 1.18   |
| HGST      | HUS726060ALE614    | 6 TB   | 4       | 430   | 0     | 1.18   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 7       | 430   | 0     | 1.18   |
| Seagate   | ST96812AS          | 64 GB  | 7       | 496   | 6     | 1.17   |
| WDC       | WD2000FYYZ         | 2 TB   | 2       | 1353  | 3     | 1.17   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 2       | 424   | 0     | 1.16   |
| Fujitsu   | MHY2200BH          | 200 GB | 2       | 412   | 0     | 1.13   |
| Toshiba   | MQ01ACF050         | 500 GB | 11      | 443   | 1     | 1.13   |
| HGST      | HUS722T2TALA604    | 2 TB   | 6       | 505   | 3     | 1.13   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 5       | 410   | 0     | 1.13   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 4       | 663   | 259   | 1.12   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 10      | 761   | 56    | 1.12   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 4       | 406   | 0     | 1.11   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 48      | 448   | 12    | 1.11   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 2       | 406   | 0     | 1.11   |
| Seagate   | ST9250410ASG       | 250 GB | 2       | 404   | 0     | 1.11   |
| Seagate   | ST3250310AS        | 250 GB | 8       | 1156  | 271   | 1.10   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 3       | 805   | 1     | 1.10   |
| Toshiba   | HDWG180            | 8 TB   | 2       | 400   | 0     | 1.10   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 49      | 422   | 3     | 1.09   |
| WDC       | WD15EARS-00Z5B1    | 1.5 TB | 2       | 2711  | 34    | 1.09   |
| Toshiba   | HDWD130            | 3 TB   | 12      | 417   | 1     | 1.09   |
| WDC       | WD3200BEKT-60PVMT0 | 320 GB | 3       | 605   | 331   | 1.06   |
| Toshiba   | HDWD110            | 1 TB   | 17      | 387   | 0     | 1.06   |
| Seagate   | ST31500541AS       | 1.5 TB | 7       | 998   | 173   | 1.05   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 3       | 383   | 0     | 1.05   |
| Toshiba   | MG04ACA600E        | 6 TB   | 2       | 382   | 0     | 1.05   |
| HGST      | HUS726020ALE610    | 2 TB   | 2       | 380   | 0     | 1.04   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 29      | 378   | 0     | 1.04   |
| WDC       | WD3200LPVX-60V0TT0 | 320 GB | 2       | 378   | 0     | 1.04   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 2       | 377   | 0     | 1.03   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 11      | 376   | 0     | 1.03   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 2       | 374   | 0     | 1.03   |
| WDC       | WD40NMZW-59GX6S1   | 4 TB   | 2       | 373   | 0     | 1.02   |
| Hitachi   | HTS725050A7E630    | 500 GB | 4       | 1059  | 738   | 1.02   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 27      | 371   | 0     | 1.02   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 2       | 370   | 0     | 1.02   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 2       | 369   | 0     | 1.01   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 18      | 387   | 2     | 1.00   |
| HGST      | HTS725032A7E630    | 320 GB | 8       | 701   | 18    | 1.00   |
| Hitachi   | HTS545050B9A300    | 500 GB | 6       | 1139  | 1111  | 0.99   |
| Hitachi   | HTS545032B9A300    | 320 GB | 9       | 436   | 267   | 0.99   |
| Seagate   | ST500LX025-1U717D  | 500 GB | 2       | 355   | 0     | 0.97   |
| Seagate   | ST14000NM001G-2... | 14 TB  | 5       | 418   | 1     | 0.97   |
| Toshiba   | MQ01ABD075         | 752 GB | 6       | 687   | 314   | 0.97   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 2       | 351   | 0     | 0.96   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 3       | 466   | 3     | 0.96   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 2       | 350   | 0     | 0.96   |
| WDC       | WD2500BEVS-22UST0  | 250 GB | 4       | 374   | 2     | 0.96   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 9       | 358   | 1     | 0.95   |
| Toshiba   | MN07ACA12T         | 12 TB  | 2       | 345   | 0     | 0.95   |
| Toshiba   | MK1637GSX          | 160 GB | 2       | 886   | 1     | 0.94   |
| Samsung   | HM321HI            | 320 GB | 6       | 373   | 145   | 0.94   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 10      | 414   | 2     | 0.93   |
| Toshiba   | HDWE160            | 6 TB   | 4       | 340   | 0     | 0.93   |
| WDC       | WD5000BPVT-22HXZT3 | 500 GB | 2       | 881   | 510   | 0.93   |
| Seagate   | ST3250410AS        | 250 GB | 5       | 615   | 4     | 0.92   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 22      | 351   | 76    | 0.92   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 4       | 334   | 0     | 0.92   |
| Hitachi   | HTS723232A7A364    | 320 GB | 7       | 954   | 462   | 0.91   |
| Seagate   | ST3250310NS        | 250 GB | 2       | 570   | 1     | 0.91   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 3       | 332   | 0     | 0.91   |
| Toshiba   | MQ01UBD100         | 1 TB   | 2       | 567   | 1     | 0.91   |
| Seagate   | ST9250827AS        | 250 GB | 6       | 524   | 201   | 0.91   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 3       | 2055  | 10    | 0.90   |
| Seagate   | ST9160310AS        | 160 GB | 2       | 1388  | 2     | 0.89   |
| MediaMax  | WL2000GSA6454      | 2 TB   | 3       | 697   | 6     | 0.89   |
| Toshiba   | MK3259GSXP         | 320 GB | 2       | 656   | 164   | 0.89   |
| HGST      | HTS545050A7E680    | 500 GB | 12      | 371   | 86    | 0.88   |
| WDC       | WD5000LPCX-24C6HT0 | 500 GB | 5       | 319   | 0     | 0.87   |
| WDC       | WD3200BPVT-75JJ5T0 | 320 GB | 2       | 720   | 2     | 0.87   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 2       | 678   | 8     | 0.87   |
| Hitachi   | HTS543232L9A300    | 320 GB | 2       | 315   | 0     | 0.87   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 16      | 315   | 0     | 0.87   |
| Toshiba   | MK2546GSX          | 250 GB | 4       | 538   | 11    | 0.86   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 4       | 310   | 0     | 0.85   |
| WDC       | WD60EFRX-68TGBN1   | 6 TB   | 3       | 2362  | 7     | 0.84   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 7       | 303   | 0     | 0.83   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 2       | 302   | 0     | 0.83   |
| Toshiba   | MQ04UBF100         | 1 TB   | 2       | 299   | 0     | 0.82   |
| Seagate   | ST9250315AS        | 250 GB | 6       | 438   | 170   | 0.82   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 5       | 380   | 2     | 0.80   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 3       | 291   | 0     | 0.80   |
| Toshiba   | MK3265GSXN         | 320 GB | 2       | 642   | 6     | 0.79   |
| Hitachi   | HTS547550A9E384    | 500 GB | 9       | 485   | 131   | 0.79   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 9       | 286   | 0     | 0.78   |
| Samsung   | HM320II            | 320 GB | 5       | 628   | 1     | 0.78   |
| WDC       | WD20EFZX-68AWUN0   | 2 TB   | 2       | 285   | 0     | 0.78   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 2       | 512   | 1     | 0.78   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 2       | 1587  | 6     | 0.77   |
| Toshiba   | MK6475GSX          | 640 GB | 3       | 1202  | 32    | 0.76   |
| WDC       | WD10SPZX-17Z10T1   | 1 TB   | 2       | 276   | 0     | 0.76   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 11      | 1399  | 735   | 0.76   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 5       | 434   | 2     | 0.75   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 4       | 682   | 244   | 0.75   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 5       | 273   | 0     | 0.75   |
| Toshiba   | MQ01ABD100         | 1 TB   | 39      | 396   | 155   | 0.74   |
| WDC       | WD3200AAJS-00L7A0  | 320 GB | 2       | 1072  | 4     | 0.74   |
| Toshiba   | MQ03UBB200         | 2 TB   | 2       | 269   | 0     | 0.74   |
| WDC       | WD10JMVW-11AJGS1   | 1 TB   | 2       | 988   | 5     | 0.74   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 19      | 310   | 73    | 0.72   |
| Seagate   | ST1000VM002-1SD102 | 1 TB   | 4       | 585   | 3     | 0.71   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 20      | 257   | 0     | 0.71   |
| WDC       | WD3200BPVT-24JJ5T0 | 320 GB | 2       | 256   | 0     | 0.70   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 20      | 575   | 346   | 0.70   |
| Samsung   | HN-M101MBB         | 1 TB   | 2       | 255   | 0     | 0.70   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 3       | 667   | 3     | 0.70   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 3       | 394   | 24    | 0.70   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 7       | 458   | 156   | 0.69   |
| Toshiba   | MG06ACA800E        | 8 TB   | 7       | 251   | 0     | 0.69   |
| Hitachi   | HDS721616PLA380    | 160 GB | 5       | 953   | 289   | 0.68   |
| WDC       | WD1600BEVS-08VAT2  | 160 GB | 3       | 404   | 1     | 0.68   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 4       | 247   | 1     | 0.67   |
| Seagate   | ST980811AS         | 80 GB  | 2       | 243   | 0     | 0.67   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 45      | 290   | 50    | 0.66   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 8       | 434   | 109   | 0.66   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 6       | 574   | 211   | 0.66   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| HP          | 6      | 23      | 2302  | 2     | 4.70   |
| Hitachi     | 70     | 339     | 1431  | 145   | 2.92   |
| HPE         | 4      | 29      | 979   | 1     | 2.66   |
| WDC         | 292    | 1513    | 1093  | 27    | 2.49   |
| Samsung     | 26     | 148     | 1401  | 189   | 2.44   |
| HGST        | 36     | 283     | 1010  | 122   | 2.41   |
| Lenovo      | 1      | 4       | 802   | 0     | 2.20   |
| Maxtor      | 6      | 17      | 923   | 131   | 2.08   |
| ExcelStor   | 2      | 4       | 1009  | 8     | 1.64   |
| Seagate     | 180    | 1513    | 816   | 135   | 1.62   |
| Fujitsu     | 5      | 11      | 545   | 0     | 1.49   |
| Toshiba     | 64     | 432     | 563   | 56    | 1.25   |
| Apple       | 3      | 12      | 453   | 5     | 1.00   |
| MediaMax    | 1      | 3       | 697   | 6     | 0.89   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

See top 1000 of tested SSD models in the [Top1000_SSD.md](/Top1000_SSD.md).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Corsair   | Force 3 SSD        | 240 GB | 2       | 2608  | 0     | 7.15   |
| Intel     | SSDMCEAC120B3      | 120 GB | 2       | 2427  | 0     | 6.65   |
| Intel     | SSDSC2BA100G3L     | 100 GB | 4       | 2369  | 0     | 6.49   |
| Apple     | SSD SM512E         | 500 GB | 2       | 2341  | 0     | 6.41   |
| Intel     | SSDSC2BB160G4      | 160 GB | 2       | 2340  | 0     | 6.41   |
| OCZ       | AGILITY            | 32 GB  | 2       | 2269  | 0     | 6.22   |
| Intel     | SSDSC2BB240G6      | 240 GB | 3       | 2265  | 0     | 6.21   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 2       | 2205  | 0     | 6.04   |
| HPE       | MK0400GCTZA        | 400 GB | 2       | 2203  | 0     | 6.04   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 5       | 2088  | 0     | 5.72   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 2       | 2007  | 0     | 5.50   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 2       | 2627  | 1     | 5.48   |
| ADATA     | SP310              | 32 GB  | 2       | 1914  | 0     | 5.25   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 15      | 1855  | 136   | 4.94   |
| Intel     | SSDSC2BP240G4      | 240 GB | 3       | 1783  | 0     | 4.89   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 2       | 1756  | 0     | 4.81   |
| Micron    | M600_MTFDDAK128MBF | 128 GB | 2       | 1741  | 0     | 4.77   |
| Intel     | SSDSA2CW120G3      | 120 GB | 7       | 1679  | 0     | 4.60   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 2       | 1664  | 0     | 4.56   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 15      | 1661  | 0     | 4.55   |
| OCZ       | VERTEX4            | 256 GB | 3       | 1660  | 0     | 4.55   |
| Samsung   | SSD 840 EVO        | 120 GB | 35      | 1799  | 12    | 4.41   |
| Samsung   | SSD 830 Series     | 256 GB | 3       | 1582  | 0     | 4.34   |
| Corsair   | Force 3 SSD        | 64 GB  | 5       | 1572  | 0     | 4.31   |
| SanDisk   | SDSSDXP480G        | 480 GB | 2       | 1552  | 0     | 4.25   |
| Intel     | SSDMCEAC030B3      | 32 GB  | 6       | 1529  | 0     | 4.19   |
| Apple     | SSD TS128C         | 121 GB | 3       | 1519  | 0     | 4.16   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 3       | 1483  | 0     | 4.06   |
| Samsung   | MZ-5EA2000-0D3     | 200 GB | 4       | 1481  | 0     | 4.06   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 3       | 1479  | 0     | 4.05   |
| Seagate   | XF1230-1A0240      | 240 GB | 2       | 1476  | 0     | 4.05   |
| Intel     | SSDSC2BB080G6      | 80 GB  | 2       | 1466  | 0     | 4.02   |
| OCZ       | VERTEX3 MI         | 120 GB | 2       | 2104  | 1     | 3.97   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 2       | 1416  | 0     | 3.88   |
| Intel     | SSDSC2CT180A3      | 180 GB | 4       | 1901  | 1     | 3.88   |
| Kingston  | SVP200S3120G       | 120 GB | 2       | 1411  | 0     | 3.87   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 15      | 1407  | 0     | 3.86   |
| Crucial   | FCCT128M4SSD1      | 128 GB | 2       | 1406  | 0     | 3.85   |
| Intel     | SSDSC2CT180A4      | 180 GB | 3       | 1870  | 1     | 3.82   |
| Samsung   | SSD 840 EVO        | 500 GB | 7       | 1474  | 120   | 3.82   |
| Toshiba   | THNSNJ128GCSY      | 128 GB | 2       | 1388  | 0     | 3.80   |
| Samsung   | SSD 840 Series     | 250 GB | 8       | 1377  | 0     | 3.78   |
| HP        | FK0032CAAZP        | 32 GB  | 3       | 1371  | 0     | 3.76   |
| Seagate   | ST240HM000-1G5152  | 240 GB | 2       | 1356  | 0     | 3.72   |
| ADATA     | SP900              | 64 GB  | 3       | 1342  | 0     | 3.68   |
| Samsung   | SSD 830 Series     | 128 GB | 15      | 1331  | 0     | 3.65   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 3       | 1550  | 341   | 3.57   |
| Kingston  | SVP200S37A60G      | 64 GB  | 5       | 1297  | 0     | 3.56   |
| Samsung   | MZ7LM240HCGR-0E003 | 240 GB | 2       | 1295  | 0     | 3.55   |
| Samsung   | MZNLN256HCHP-000H1 | 256 GB | 3       | 1286  | 0     | 3.53   |
| Corsair   | Force GS           | 128 GB | 2       | 1279  | 0     | 3.51   |
| HPE       | MK000480GWCEV      | 480 GB | 2       | 1275  | 0     | 3.49   |
| HPE       | MK000960GWCFA      | 960 GB | 2       | 1275  | 0     | 3.49   |
| Seagate   | XF1230-1A0480      | 480 GB | 2       | 1266  | 0     | 3.47   |
| Intel     | SSDSA2CW160G3      | 160 GB | 5       | 1263  | 0     | 3.46   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 3       | 1430  | 1     | 3.45   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 2       | 1260  | 0     | 3.45   |
| Toshiba   | THNSNH128GBST      | 128 GB | 3       | 1234  | 0     | 3.38   |
| Samsung   | SSD CM871 2.5 7mm  | 128 GB | 2       | 1228  | 0     | 3.37   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 2       | 1224  | 0     | 3.35   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 12      | 1424  | 84    | 3.35   |
| PNY       | CS1311 240GB SSD   | 240 GB | 5       | 1217  | 0     | 3.33   |
| Samsung   | SSD 850 PRO        | 128 GB | 13      | 1215  | 0     | 3.33   |
| OCZ       | AGILITY3           | 120 GB | 10      | 1238  | 121   | 3.32   |
| SanDisk   | Ultra II           | 960 GB | 2       | 1202  | 0     | 3.29   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 3       | 1180  | 0     | 3.24   |
| Intel     | SSDSC2BB960G7R     | 960 GB | 6       | 1177  | 0     | 3.23   |
| Samsung   | SSD PB22-JS3 FD... | 128 GB | 2       | 1176  | 0     | 3.22   |
| Dell      | SSDSCKJB120G7R     | 120 GB | 2       | 1173  | 0     | 3.22   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 1154  | 0     | 3.16   |
| Intel     | SSDSC2BB120G4      | 120 GB | 17      | 1212  | 1     | 3.13   |
| Samsung   | SSD 840 PRO Series | 128 GB | 19      | 1248  | 86    | 3.11   |
| Kingston  | SUV300S37A240G     | 240 GB | 2       | 1135  | 0     | 3.11   |
| Samsung   | SSD 840 Series     | 120 GB | 20      | 1218  | 52    | 3.10   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 3       | 1128  | 0     | 3.09   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 2       | 1125  | 0     | 3.08   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 2       | 1117  | 0     | 3.06   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 3       | 1111  | 0     | 3.05   |
| Patriot   | Flare              | 64 GB  | 2       | 1107  | 0     | 3.03   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 2       | 1226  | 1     | 3.03   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 5       | 1102  | 0     | 3.02   |
| ADATA     | SP600              | 32 GB  | 2       | 1097  | 0     | 3.01   |
| OCZ       | VERTEX3            | 64 GB  | 4       | 1741  | 8     | 2.97   |
| Intel     | SSDSC2CW240A3      | 240 GB | 7       | 1083  | 0     | 2.97   |
| SanDisk   | SDSA6PM-064G-1006  | 64 GB  | 2       | 1064  | 0     | 2.92   |
| Kingston  | SKC400S37512G      | 512 GB | 2       | 1059  | 0     | 2.90   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 2       | 1056  | 0     | 2.90   |
| Kingston  | SNV425S2128GB      | 128 GB | 3       | 2111  | 6     | 2.86   |
| Intel     | SSDSC2BA400G4      | 400 GB | 3       | 1508  | 1     | 2.85   |
| Intel     | SSDSC2KB240G7      | 240 GB | 3       | 1031  | 0     | 2.82   |
| Kingston  | SMS200S330G        | 32 GB  | 9       | 1140  | 1     | 2.79   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 4       | 1293  | 522   | 2.77   |
| Crucial   | CT250MX200SSD1     | 250 GB | 5       | 1078  | 1     | 2.76   |
| Patriot   | Blaze              | 64 GB  | 2       | 1006  | 0     | 2.76   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 6       | 997   | 0     | 2.73   |
| Crucial   | CT240M500SSD3      | 240 GB | 3       | 985   | 0     | 2.70   |
| Goodram   | SSD                | 240 GB | 4       | 983   | 0     | 2.70   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 3       | 969   | 0     | 2.66   |
| Samsung   | SSD 850 EVO        | 120 GB | 30      | 960   | 0     | 2.63   |
| Crucial   | CT128M550SSD1      | 128 GB | 2       | 1528  | 2     | 2.62   |
| Samsung   | MZNLN512HMJP-000H1 | 512 GB | 2       | 955   | 0     | 2.62   |
| Transcend | TS64GMTS400S       | 64 GB  | 3       | 954   | 0     | 2.61   |
| Samsung   | SSD 750 EVO        | 120 GB | 10      | 952   | 0     | 2.61   |
| OCZ       | VERTEX4            | 128 GB | 5       | 1130  | 1     | 2.61   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 6       | 940   | 0     | 2.58   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 5       | 936   | 0     | 2.56   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 2       | 935   | 0     | 2.56   |
| AMD       | R3SL120G           | 120 GB | 3       | 933   | 0     | 2.56   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 2       | 1458  | 1     | 2.52   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 2       | 911   | 0     | 2.50   |
| Samsung   | SSD 750 EVO        | 250 GB | 11      | 903   | 0     | 2.48   |
| Samsung   | SSD 840 EVO        | 250 GB | 37      | 900   | 0     | 2.47   |
| Crucial   | CT250MX200SSD3     | 250 GB | 2       | 892   | 0     | 2.45   |
| SuperM... | SSD                | 64 GB  | 4       | 889   | 0     | 2.44   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 5       | 887   | 0     | 2.43   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 6       | 885   | 0     | 2.43   |
| HPE       | MK000240GWEZF      | 240 GB | 2       | 882   | 0     | 2.42   |
| Samsung   | SSD 830 Series     | 64 GB  | 4       | 878   | 0     | 2.41   |
| Innodisk  | DEMSR- 08GB mSA... | 8 GB   | 3       | 876   | 0     | 2.40   |
| Kingston  | SNV425S264GB       | 64 GB  | 2       | 882   | 3     | 2.40   |
| Kingston  | SH103S3120G        | 120 GB | 6       | 874   | 0     | 2.40   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 14      | 868   | 0     | 2.38   |
| OCZ       | AGILITY3           | 64 GB  | 6       | 1028  | 1     | 2.36   |
| Intel     | SSDSC2BB150G7      | 150 GB | 7       | 924   | 1     | 2.32   |
| WDC       | WDBNCE5000PNC      | 500 GB | 5       | 845   | 0     | 2.32   |
| Samsung   | SSD 840 PRO Series | 256 GB | 20      | 1199  | 62    | 2.31   |
| Samsung   | SSD 850 EVO        | 500 GB | 62      | 876   | 2     | 2.30   |
| ADATA     | SSD S510           | 64 GB  | 2       | 839   | 0     | 2.30   |
| Micron    | P300-MTFDDAC100SAL | 100 GB | 2       | 1551  | 503   | 2.30   |
| Intel     | SSDSCKHB120G4      | 120 GB | 2       | 834   | 0     | 2.29   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 2       | 831   | 0     | 2.28   |
| Samsung   | SSD 850 PRO        | 512 GB | 19      | 827   | 0     | 2.27   |
| Intel     | SSDSC2BB480G7      | 480 GB | 3       | 940   | 1     | 2.26   |
| Samsung   | SSD 850 EVO        | 250 GB | 121     | 847   | 1     | 2.25   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 6       | 820   | 0     | 2.25   |
| ADATA     | SP920SS            | 128 GB | 2       | 816   | 0     | 2.24   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 2       | 816   | 0     | 2.24   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 2       | 814   | 0     | 2.23   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 18      | 814   | 0     | 2.23   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 12      | 813   | 0     | 2.23   |
| Apple     | SSD SM0512F        | 500 GB | 2       | 812   | 0     | 2.23   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 7       | 804   | 0     | 2.21   |
| Toshiba   | THNSFJ256GDNU      | 256 GB | 3       | 803   | 0     | 2.20   |
| Samsung   | SSD 850 EVO        | 1 TB   | 17      | 1028  | 1     | 2.18   |
| Crucial   | CT960M500SSD1      | 960 GB | 2       | 787   | 0     | 2.16   |
| SanDisk   | SSD PLUS 120 GB    | 120 GB | 4       | 843   | 1     | 2.16   |
| Kingston  | SV300S37A120G      | 120 GB | 58      | 981   | 2     | 2.14   |
| Kingston  | SUV400S37240G      | 240 GB | 11      | 837   | 1     | 2.14   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 5       | 778   | 0     | 2.13   |
| Goodram   | SSD                | 120 GB | 6       | 775   | 0     | 2.12   |
| Intel     | SSDSC2KG240G7      | 240 GB | 2       | 1289  | 2     | 2.12   |
| Samsung   | MZMTE128HMGR-00007 | 128 GB | 3       | 869   | 1     | 2.12   |
| Corsair   | Force GT           | 120 GB | 3       | 1165  | 2     | 2.12   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 2       | 1119  | 165   | 2.12   |
| China     | SATA SSD           | 16 GB  | 74      | 765   | 0     | 2.10   |
| Samsung   | SSD 850 PRO        | 256 GB | 27      | 809   | 1     | 2.09   |
| Toshiba   | Q300               | 480 GB | 2       | 762   | 0     | 2.09   |
| OCZ       | VERTEX3            | 120 GB | 8       | 1218  | 21    | 2.09   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 2       | 760   | 0     | 2.08   |
| Samsung   | SSD 850 EVO        | 2 TB   | 2       | 759   | 0     | 2.08   |
| Samsung   | MZYLN256HCHP-000L2 | 256 GB | 2       | 758   | 0     | 2.08   |
| OCZ       | VERTEX460A         | 120 GB | 2       | 752   | 0     | 2.06   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 2       | 743   | 0     | 2.04   |
| Phison    | SATA SSD           | 120 GB | 4       | 741   | 0     | 2.03   |
| Samsung   | SSD RBX Series ... | 64 GB  | 2       | 739   | 0     | 2.03   |
| Samsung   | SSD 840 PRO Series | 512 GB | 4       | 736   | 0     | 2.02   |
| Protectli | 16GB mSATA         | 16 GB  | 2       | 728   | 0     | 2.00   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 2       | 727   | 0     | 1.99   |
| OCZ       | ARC100             | 240 GB | 3       | 726   | 0     | 1.99   |
| SanDisk   | SSD U100           | 24 GB  | 3       | 724   | 0     | 1.98   |
| SanDisk   | SDSSDP064G         | 64 GB  | 10      | 729   | 1     | 1.98   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 3       | 721   | 0     | 1.98   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 2       | 712   | 0     | 1.95   |
| Samsung   | MZ7LN256HAJQ-000L7 | 256 GB | 2       | 712   | 0     | 1.95   |
| Intel     | SSDSC2BW120A4      | 120 GB | 15      | 710   | 0     | 1.95   |
| PNY       | CS1311 120GB SSD   | 120 GB | 4       | 794   | 1     | 1.94   |
| SanDisk   | SDSSDHP128G        | 128 GB | 2       | 706   | 0     | 1.93   |
| Samsung   | SSD 860 EVO        | 2 TB   | 4       | 701   | 0     | 1.92   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 2       | 700   | 0     | 1.92   |
| SanDisk   | SDSSDHII240G       | 240 GB | 2       | 700   | 0     | 1.92   |
| Kingston  | SV300S37A480G      | 480 GB | 2       | 695   | 0     | 1.91   |
| KingSpec  | NT-32              | 32 GB  | 2       | 690   | 0     | 1.89   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 10      | 687   | 0     | 1.88   |
| Kingston  | SHFS37A120G        | 120 GB | 10      | 894   | 1     | 1.88   |
| Crucial   | CT256MX100SSD1     | 256 GB | 10      | 685   | 0     | 1.88   |
| ADATA     | SP600              | 64 GB  | 2       | 683   | 0     | 1.87   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 2       | 680   | 0     | 1.87   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 6       | 675   | 0     | 1.85   |
| ADATA     | SP600              | 128 GB | 2       | 673   | 0     | 1.84   |
| Transcend | TS64GSSD340        | 64 GB  | 2       | 672   | 0     | 1.84   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 2       | 671   | 0     | 1.84   |
| Intel     | SSDSC2BX400G4      | 400 GB | 2       | 666   | 0     | 1.83   |
| Intel     | SSDMCEAC060B3      | 64 GB  | 4       | 810   | 1     | 1.83   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 5       | 736   | 1     | 1.81   |
| ADATA     | IM2S3134N-064GM    | 64 GB  | 23      | 660   | 0     | 1.81   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 2       | 658   | 0     | 1.80   |
| Goodram   | SSDPR-CX400-128    | 128 GB | 3       | 657   | 0     | 1.80   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 6       | 853   | 1     | 1.80   |
| SanDisk   | SSD U100           | 16 GB  | 8       | 653   | 0     | 1.79   |
| Corsair   | Force LS SSD       | 64 GB  | 6       | 1019  | 169   | 1.79   |
| SPCC      | SSD                | 64 GB  | 6       | 649   | 0     | 1.78   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 2       | 646   | 0     | 1.77   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 4       | 637   | 0     | 1.75   |
| Kingston  | SM2280S3120G       | 120 GB | 3       | 633   | 0     | 1.74   |
| Corsair   | Force GS           | 180 GB | 2       | 631   | 0     | 1.73   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 4       | 625   | 0     | 1.71   |
| Kingston  | SS200S330G         | 32 GB  | 3       | 624   | 0     | 1.71   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 3       | 623   | 0     | 1.71   |
| Kingston  | SMS200S360G        | 64 GB  | 15      | 1155  | 143   | 1.71   |
| Kingston  | SH103S3240G        | 240 GB | 4       | 1059  | 453   | 1.69   |
| SanDisk   | SD8SB8U-256G-1006  | 256 GB | 2       | 616   | 0     | 1.69   |
| Transcend | TS128GSSD230S      | 128 GB | 3       | 611   | 0     | 1.68   |
| SanDisk   | SSD i100           | 32 GB  | 3       | 1045  | 4     | 1.67   |
| Crucial   | CT1050MX300SSD4    | 1 TB   | 3       | 1520  | 4     | 1.67   |
| Kingston  | SUV500120G         | 120 GB | 3       | 608   | 0     | 1.67   |
| Crucial   | CT275MX300SSD4     | 275 GB | 5       | 636   | 35    | 1.63   |
| Kingston  | SUV400S37120G      | 120 GB | 19      | 624   | 50    | 1.61   |
| Intel     | SSDSC2BB012T7      | 1.2 TB | 2       | 1169  | 1     | 1.60   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 2       | 580   | 0     | 1.59   |
| Advantech | SQF-SLMM2-8G-8SE   | 8 GB   | 3       | 577   | 0     | 1.58   |
| SanDisk   | SDSSDP128G         | 128 GB | 11      | 572   | 0     | 1.57   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 4       | 568   | 0     | 1.56   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 7       | 1845  | 581   | 1.54   |
| SK hynix  | SC311 SATA         | 256 GB | 8       | 556   | 0     | 1.53   |
| Samsung   | SSD 840 Series     | 500 GB | 4       | 686   | 1     | 1.52   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 4       | 553   | 0     | 1.52   |
| OWC       | Mercury Electra... | 240 GB | 3       | 552   | 0     | 1.51   |
| TCSUNBOW  | M1                 | 32 GB  | 5       | 552   | 0     | 1.51   |
| Kingston  | SV300S37A60G       | 64 GB  | 23      | 1076  | 39    | 1.51   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 2       | 550   | 0     | 1.51   |
| Intel     | SSDMCEAW120A4      | 120 GB | 4       | 550   | 0     | 1.51   |
| Intel     | SSDSC2CT120A3      | 120 GB | 8       | 1015  | 2     | 1.50   |
| Corsair   | Force 3 SSD        | 120 GB | 6       | 974   | 169   | 1.50   |
| Intel     | SSDSC2BW240H6      | 240 GB | 4       | 546   | 0     | 1.50   |
| Phison    | SATA SSD           | 16 GB  | 45      | 544   | 0     | 1.49   |
| OCZ       | VERTEX3            | 240 GB | 2       | 1232  | 511   | 1.48   |
| Hoodisk   | SSD                | 16 GB  | 18      | 540   | 0     | 1.48   |
| SK hynix  | SC311 SATA         | 128 GB | 4       | 539   | 0     | 1.48   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 3       | 539   | 0     | 1.48   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 3       | 539   | 0     | 1.48   |
| SanDisk   | SDSSDHII120G       | 120 GB | 4       | 534   | 0     | 1.46   |
| Hoodisk   | SSD                | 32 GB  | 56      | 531   | 0     | 1.46   |
| Samsung   | SSD 860 EVO        | 4 TB   | 2       | 527   | 0     | 1.45   |
| SanDisk   | SSD i110           | 32 GB  | 3       | 1121  | 340   | 1.44   |
| SanDisk   | SDSSDH3500G        | 500 GB | 2       | 524   | 0     | 1.44   |
| SanDisk   | X400 M.2 2280      | 128 GB | 8       | 523   | 0     | 1.43   |
| SanDisk   | Ultra II           | 480 GB | 5       | 520   | 0     | 1.42   |
| Transcend | TS32GSSD340K       | 32 GB  | 2       | 518   | 0     | 1.42   |
| Crucial   | CT250MX200SSD4     | 250 GB | 2       | 515   | 0     | 1.41   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 5       | 513   | 0     | 1.41   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 10      | 2030  | 6     | 1.40   |
| Intenso   | SSD Sata III       | 120 GB | 6       | 510   | 0     | 1.40   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 4       | 510   | 0     | 1.40   |
| Apple     | SSD SM0512G        | 500 GB | 4       | 509   | 0     | 1.40   |
| Kingston  | SV300S37A240G      | 240 GB | 15      | 659   | 2     | 1.39   |
| WDC       | WDBNCE2500PNC      | 250 GB | 4       | 505   | 0     | 1.39   |
| Kingston  | SMS200S3120G       | 120 GB | 15      | 1107  | 12    | 1.38   |
| Crucial   | CT250MX500SSD4     | 250 GB | 4       | 503   | 0     | 1.38   |
| Lite-On   | LCH-128V2S-11 2... | 128 GB | 2       | 500   | 0     | 1.37   |
| Protectli | 480GB mSATA        | 480 GB | 2       | 499   | 0     | 1.37   |
| Intel     | SSDSC2KW256G8      | 256 GB | 12      | 504   | 1     | 1.36   |
| SanDisk   | SDSSDA120G         | 120 GB | 32      | 499   | 23    | 1.35   |
| Toshiba   | Q300 Pro           | 128 GB | 2       | 494   | 0     | 1.35   |
| Smartbuy  | SSD                | 120 GB | 2       | 494   | 0     | 1.35   |
| ADATA     | SP900              | 128 GB | 7       | 493   | 0     | 1.35   |
| SanDisk   | X400 M.2 2280      | 256 GB | 5       | 492   | 0     | 1.35   |
| China     | M10C               | 256 GB | 2       | 492   | 0     | 1.35   |
| Innodisk  | DEMSR- 16GB mSA... | 16 GB  | 6       | 492   | 0     | 1.35   |
| SanDisk   | SD8TB8U512G1001    | 512 GB | 2       | 489   | 0     | 1.34   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 2       | 488   | 0     | 1.34   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 2       | 482   | 0     | 1.32   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 3       | 476   | 0     | 1.30   |
| Crucial   | CT240M500SSD1      | 240 GB | 8       | 1020  | 337   | 1.30   |
| Intel     | SSDSC2BW180A4      | 180 GB | 10      | 474   | 0     | 1.30   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 2       | 472   | 0     | 1.29   |
| Samsung   | SSD 750 EVO        | 500 GB | 2       | 471   | 0     | 1.29   |
| Kingston  | SUV500MS120G       | 120 GB | 64      | 469   | 0     | 1.29   |
| Samsung   | MZ7LN128HCHP-00000 | 128 GB | 2       | 467   | 0     | 1.28   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 4       | 466   | 0     | 1.28   |
| Samsung   | MZNLN512HMJP-000L7 | 512 GB | 2       | 465   | 0     | 1.28   |
| China     | SATA SSD           | 120 GB | 21      | 458   | 0     | 1.26   |
| KingFast  | SSD                | 16 GB  | 6       | 458   | 0     | 1.26   |
| SPCC      | SSD                | 1 TB   | 21      | 456   | 0     | 1.25   |
| Apacer    | 128GB SATA Flas... | 128 GB | 3       | 456   | 0     | 1.25   |
| OCZ       | VERTEX2            | 120 GB | 2       | 455   | 0     | 1.25   |
| Patriot   | Burst              | 480 GB | 2       | 455   | 0     | 1.25   |
| Apacer    | AS350              | 120 GB | 2       | 453   | 0     | 1.24   |
| Crucial   | CT525MX300SSD1     | 528 GB | 17      | 634   | 2     | 1.23   |
| Kingston  | RBUSNS8180DS3128GH | 128 GB | 3       | 448   | 0     | 1.23   |
| Micron    | 5200_MTFDDAK1T9TDN | 1.9 TB | 2       | 446   | 0     | 1.22   |
| Hoodisk   | SSD                | 64 GB  | 57      | 446   | 0     | 1.22   |
| Intel     | SSDSC2BF180A4H     | 180 GB | 4       | 445   | 0     | 1.22   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 7       | 509   | 1     | 1.22   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 4       | 441   | 0     | 1.21   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 8       | 439   | 0     | 1.20   |
| Samsung   | SSD 650            | 120 GB | 2       | 438   | 0     | 1.20   |
| Phison    | SATA SSD           | 128 GB | 5       | 438   | 0     | 1.20   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 2       | 436   | 0     | 1.20   |
| SPCC      | SSD                | 120 GB | 10      | 435   | 0     | 1.19   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 2       | 433   | 0     | 1.19   |
| SanDisk   | Ultra II           | 240 GB | 2       | 433   | 0     | 1.19   |
| Apacer    | 32GB SATA Flash... | 32 GB  | 11      | 601   | 104   | 1.18   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 3       | 430   | 0     | 1.18   |
| Kingston  | SUV400S37480G      | 480 GB | 3       | 847   | 4     | 1.18   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 7       | 444   | 2     | 1.16   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 6       | 793   | 20    | 1.16   |
| OCZ       | TRION100           | 240 GB | 2       | 422   | 0     | 1.16   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 5       | 422   | 0     | 1.16   |
| SK hynix  | SC311 SATA         | 512 GB | 3       | 420   | 0     | 1.15   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 2       | 419   | 0     | 1.15   |
| Samsung   | SSD 860 EVO        | 500 GB | 76      | 417   | 0     | 1.14   |
| Hoodisk   | SSD                | 128 GB | 53      | 417   | 0     | 1.14   |
| Samsung   | MZ7LH480HAHQ-00005 | 480 GB | 2       | 417   | 0     | 1.14   |
| Intel     | SSDSC2BP480G4      | 480 GB | 2       | 415   | 0     | 1.14   |
| Transcend | TS128GSSD370S      | 128 GB | 3       | 413   | 0     | 1.13   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 2       | 885   | 8     | 1.13   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 2       | 406   | 0     | 1.11   |
| SanDisk   | SDSSDH3 1T02       | 1 TB   | 2       | 406   | 0     | 1.11   |
| MyDigi... | SB2                | 128 GB | 4       | 658   | 2     | 1.09   |
| Apple     | SSD TS256C         | 256 GB | 2       | 566   | 4     | 1.09   |
| Intel     | SSDSC2BW180A3H     | 180 GB | 2       | 397   | 0     | 1.09   |
| Samsung   | SSD 840 EVO        | 1 TB   | 5       | 396   | 0     | 1.09   |
| Intel     | SSDSC2BW120A3      | 120 GB | 2       | 991   | 508   | 1.08   |
| PNY       | CS900 120GB SSD    | 120 GB | 40      | 395   | 0     | 1.08   |
| Samsung   | MZMPC032HBCD-000L1 | 32 GB  | 2       | 388   | 0     | 1.07   |
| Toshiba   | TR200              | 240 GB | 8       | 388   | 0     | 1.07   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 2       | 387   | 0     | 1.06   |
| SanDisk   | SSD U100           | 128 GB | 2       | 386   | 0     | 1.06   |
| Samsung   | MZ7LM240HMHQ-00005 | 240 GB | 2       | 385   | 0     | 1.05   |
| ADATA     | SU750              | 256 GB | 3       | 381   | 0     | 1.04   |
| Samsung   | SSD 860 QVO        | 1 TB   | 15      | 380   | 0     | 1.04   |
| Crucial   | CT120BX500SSD1     | 120 GB | 50      | 378   | 0     | 1.04   |
| Samsung   | Portable SSD T5    | 500 GB | 4       | 376   | 0     | 1.03   |
| SanDisk   | SDSSDHII960G       | 960 GB | 2       | 371   | 0     | 1.02   |
| Zheino    | CHN-mSATAM3-256    | 256 GB | 2       | 371   | 0     | 1.02   |
| SanDisk   | SDSSDA240G         | 240 GB | 24      | 404   | 4     | 1.01   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 2       | 368   | 0     | 1.01   |
| Samsung   | SSD 860 PRO        | 256 GB | 21      | 366   | 0     | 1.00   |
| Patriot   | Burst              | 240 GB | 11      | 366   | 0     | 1.00   |
| SanDisk   | SD8TN8U256G1001    | 256 GB | 2       | 365   | 0     | 1.00   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 2       | 364   | 0     | 1.00   |
| Apacer    | 64GB SATA Flash... | 64 GB  | 10      | 406   | 20    | 1.00   |
| Samsung   | SSD 860 PRO        | 1 TB   | 6       | 361   | 0     | 0.99   |
| Transcend | TS128GMTS400       | 128 GB | 2       | 360   | 0     | 0.99   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 14      | 357   | 0     | 0.98   |
| Kingston  | SHFS37A240G        | 240 GB | 8       | 356   | 0     | 0.98   |
| SanDisk   | SDEZS25-240G-Z01   | 240 GB | 2       | 355   | 0     | 0.97   |
| Hoodisk   | SSD                | 512 GB | 4       | 355   | 0     | 0.97   |
| Intel     | SSDSC2KB240G8      | 240 GB | 19      | 352   | 0     | 0.97   |
| Transcend | 3E128-TS2-550B01   | 100 GB | 4       | 502   | 257   | 0.96   |
| SanDisk   | SSD PLUS           | 120 GB | 33      | 351   | 0     | 0.96   |
| SanDisk   | SDSSDP256G         | 256 GB | 2       | 349   | 0     | 0.96   |
| SK hynix  | SC308 SATA         | 256 GB | 5       | 710   | 17    | 0.96   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 3       | 348   | 0     | 0.96   |
| OCZ       | AGILITY4           | 128 GB | 4       | 368   | 1     | 0.95   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 4       | 346   | 0     | 0.95   |
| SanDisk   | SD6SB1M064G1022I   | 64 GB  | 6       | 343   | 0     | 0.94   |
| SanDisk   | SD7SN3Q512G1002    | 512 GB | 2       | 343   | 0     | 0.94   |
| SK hynix  | SHGS31-250GS-2     | 250 GB | 3       | 343   | 0     | 0.94   |
| KingSpec  | P4-120             | 120 GB | 3       | 343   | 0     | 0.94   |
| Samsung   | SSD 860 EVO        | 250 GB | 62      | 343   | 0     | 0.94   |
| Crucial   | CT960BX500SSD1     | 960 GB | 3       | 343   | 0     | 0.94   |
| Crucial   | CT525MX300SSD4     | 528 GB | 2       | 370   | 2     | 0.94   |
| Intenso   | SSD SATAIII        | 120 GB | 7       | 340   | 1     | 0.93   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 5       | 338   | 0     | 0.93   |
| OCZ       | TRION150           | 240 GB | 2       | 338   | 0     | 0.93   |
| China     | SATA SSD           | 128 GB | 10      | 336   | 0     | 0.92   |
| China     | SATA SSD           | 64 GB  | 13      | 436   | 9     | 0.92   |
| Samsung   | MZYLF128HCHP-000L2 | 128 GB | 3       | 334   | 0     | 0.92   |
| Gigaby... | GP-GSTFS31240GNTD  | 240 GB | 2       | 333   | 0     | 0.91   |
| Hoodisk   | SSD                | 256 GB | 11      | 331   | 0     | 0.91   |
| SanDisk   | SSD U110           | 16 GB  | 12      | 329   | 0     | 0.90   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 2       | 326   | 0     | 0.89   |
| Pioneer   | APS-SL3N-256       | 256 GB | 2       | 322   | 0     | 0.88   |
| China     | DHMSR64GD81BC1QC   | 54 GB  | 2       | 320   | 0     | 0.88   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 6       | 319   | 0     | 0.88   |
| Kingston  | SUV500MS240G       | 240 GB | 35      | 316   | 0     | 0.87   |
| KingFast  | SSD                | 120 GB | 22      | 315   | 42    | 0.86   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 4       | 1171  | 22    | 0.86   |
| ADATA     | SP900              | 256 GB | 2       | 614   | 212   | 0.85   |
| Apacer    | 16GB SATA Flash... | 16 GB  | 20      | 464   | 12    | 0.85   |
| Phison    | SATA SSD           | 32 GB  | 7       | 301   | 0     | 0.83   |
| Crucial   | CT500MX200SSD1     | 500 GB | 5       | 300   | 0     | 0.82   |
| China     | SATA SSD           | 32 GB  | 19      | 436   | 13    | 0.82   |
| Samsung   | MZMPC128HBFU-000H1 | 128 GB | 2       | 297   | 0     | 0.81   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 2       | 296   | 0     | 0.81   |
| Integral  | V Series SATA SSD  | 120 GB | 3       | 295   | 0     | 0.81   |
| Transcend | TS64GSSD370        | 64 GB  | 21      | 295   | 0     | 0.81   |
| Samsung   | SSD 850 PRO        | 1 TB   | 4       | 294   | 0     | 0.81   |
| HP        | SSD S700 Pro       | 512 GB | 2       | 294   | 0     | 0.81   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 9       | 292   | 0     | 0.80   |
| Kingston  | SA400S37120G       | 120 GB | 102     | 302   | 1     | 0.79   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 45      | 329   | 21    | 0.79   |
| Intel     | SSDSC2CW120A3      | 120 GB | 7       | 1817  | 727   | 0.78   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 20      | 292   | 1     | 0.78   |
| Protectli | 32GB mSATA         | 32 GB  | 8       | 285   | 0     | 0.78   |
| Transcend | TS32GMTS400S       | 32 GB  | 3       | 278   | 0     | 0.76   |
| SK hynix  | SHGS31-500GS-2     | 500 GB | 4       | 277   | 0     | 0.76   |
| SanDisk   | SDSSDH3512G        | 512 GB | 3       | 415   | 1     | 0.76   |
| Micron    | MTFDDAT064MAM-1J2  | 64 GB  | 2       | 277   | 0     | 0.76   |
| SanDisk   | SDSA6MM-008G-1006  | 8 GB   | 4       | 276   | 0     | 0.76   |
| ADATA     | SU650              | 960 GB | 2       | 358   | 145   | 0.76   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 22      | 274   | 0     | 0.75   |
| Samsung   | SSD 860 EVO        | 1 TB   | 46      | 274   | 1     | 0.75   |
| Patriot   | Burst              | 960 GB | 3       | 271   | 0     | 0.74   |
| China     | SATA SSD           | 512 GB | 3       | 271   | 0     | 0.74   |
| Intel     | SSDSC2BB120G4C     | 120 GB | 2       | 270   | 0     | 0.74   |
| Intel     | SSDSC2BW240A4      | 240 GB | 6       | 264   | 0     | 0.73   |
| HP        | SSD S700           | 250 GB | 5       | 264   | 0     | 0.72   |
| SanDisk   | X400 M.2 2280      | 512 GB | 2       | 263   | 0     | 0.72   |
| Patriot   | Burst              | 120 GB | 15      | 261   | 0     | 0.72   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 33      | 310   | 1     | 0.71   |
| Team      | TM8PS7512G         | 512 GB | 3       | 257   | 0     | 0.71   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 2       | 256   | 0     | 0.70   |
| Crucial   | CT275MX300SSD1     | 275 GB | 12      | 579   | 351   | 0.70   |
| Samsung   | MZNLN128HAHQ-000H1 | 128 GB | 2       | 255   | 0     | 0.70   |
| Kston     | SSD                | 128 GB | 10      | 279   | 1     | 0.70   |
| Crucial   | CT250MX500SSD1     | 250 GB | 67      | 255   | 0     | 0.70   |
| SanDisk   | SD8SN8U-128G-1006  | 128 GB | 5       | 255   | 0     | 0.70   |
| KingDian  | S280               | 240 GB | 2       | 253   | 0     | 0.69   |
| Gigaby... | GP-GSTFS31256GTND  | 256 GB | 2       | 252   | 0     | 0.69   |
| Kingston  | SA400S37960G       | 960 GB | 7       | 250   | 0     | 0.69   |
| KIOXIA... | SATA SSD           | 240 GB | 2       | 250   | 0     | 0.69   |
| Kston     | SSD                | 32 GB  | 5       | 249   | 0     | 0.68   |
| ADATA     | SU650              | 480 GB | 3       | 248   | 0     | 0.68   |
| Intel     | SSDSC2BA100G3C     | 100 GB | 2       | 247   | 0     | 0.68   |
| SanDisk   | SD5SG2128G1052E    | 128 GB | 3       | 254   | 1     | 0.68   |
| Crucial   | CT240BX500SSD1     | 240 GB | 63      | 245   | 0     | 0.67   |
| SanDisk   | SD5SE2256G1002E    | 256 GB | 3       | 290   | 1     | 0.67   |
| WDC       | WDS500G2B0A        | 500 GB | 8       | 245   | 0     | 0.67   |
| Crucial   | CT500MX500SSD4     | 500 GB | 9       | 245   | 0     | 0.67   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 8       | 314   | 1     | 0.67   |
| Crucial   | CT120M500SSD1      | 120 GB | 5       | 741   | 4     | 0.67   |
| SanDisk   | SD9TB8W512G1001    | 512 GB | 2       | 239   | 0     | 0.66   |
| Corsair   | Force LS SSD       | 120 GB | 3       | 280   | 336   | 0.65   |
| Transcend | TS120GMTS420S      | 120 GB | 18      | 237   | 0     | 0.65   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 4       | 235   | 0     | 0.64   |
| Seagate   | BarraCuda 120 S... | 500 GB | 2       | 233   | 0     | 0.64   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 4       | 233   | 0     | 0.64   |
| Kingston  | SUV500MS480G       | 480 GB | 14      | 235   | 1     | 0.64   |
| PNY       | CS900 250GB SSD    | 250 GB | 7       | 230   | 0     | 0.63   |
| China     | 256GB QLC SATA SSD | 256 GB | 3       | 230   | 0     | 0.63   |
| Samsung   | SSD 860 PRO        | 2 TB   | 2       | 229   | 0     | 0.63   |
| Crucial   | CT500MX500SSD1     | 500 GB | 58      | 234   | 1     | 0.63   |
| ORICO     | M200               | 128 GB | 2       | 226   | 0     | 0.62   |
| KingSpec  | MT-64              | 64 GB  | 2       | 225   | 0     | 0.62   |
| Kingston  | SA400S37240G       | 240 GB | 148     | 229   | 1     | 0.61   |
| Samsung   | SSD 860 PRO        | 512 GB | 13      | 223   | 0     | 0.61   |
| SanDisk   | SSD PLUS           | 1 TB   | 7       | 223   | 0     | 0.61   |
| Transcend | TS240GMTS420S      | 240 GB | 6       | 221   | 0     | 0.61   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 13      | 220   | 0     | 0.60   |
| China     | XJH-128GB          | 128 GB | 7       | 219   | 0     | 0.60   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 6       | 1173  | 9     | 0.60   |
| Kingston  | SHSS37A240G        | 240 GB | 2       | 217   | 0     | 0.60   |
| SPCC      | M.2 SSD            | 128 GB | 3       | 217   | 0     | 0.60   |
| ADATA     | SU800              | 256 GB | 10      | 219   | 201   | 0.59   |
| SPCC      | SSD                | 240 GB | 2       | 216   | 0     | 0.59   |
| Innodisk  | Corp. - mSATA 3ME3 | 32 GB  | 3       | 215   | 0     | 0.59   |
| SK hynix  | HFS256G39TND-N210A | 256 GB | 4       | 214   | 0     | 0.59   |
| Transcend | TS512GSSD370       | 512 GB | 2       | 213   | 0     | 0.58   |
| Toshiba   | Q300               | 240 GB | 2       | 212   | 0     | 0.58   |
| Samsung   | MZMPC032HBCD-000H1 | 32 GB  | 2       | 211   | 0     | 0.58   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 2       | 211   | 0     | 0.58   |
| Lite-On   | IT LCS-128L9S-HP   | 128 GB | 2       | 211   | 0     | 0.58   |
| OWC       | Mercury Electra... | 1 TB   | 6       | 210   | 0     | 0.58   |
| Apacer    | AS340              | 240 GB | 5       | 209   | 0     | 0.57   |
| FORESEE   | 32GB SSD           | 32 GB  | 4       | 209   | 0     | 0.57   |
| Intel     | SSDSC2KG480G8      | 480 GB | 8       | 291   | 1     | 0.57   |
| Wicgtyp   | M900-128           | 128 GB | 2       | 207   | 0     | 0.57   |
| Kingston  | SUV500240G         | 240 GB | 3       | 205   | 0     | 0.56   |
| China     | SATA SSD           | 240 GB | 8       | 205   | 0     | 0.56   |
| China     | C500               | 128 GB | 3       | 205   | 0     | 0.56   |
| Seagate   | FireCuda 120 SS... | 1 TB   | 2       | 204   | 0     | 0.56   |
| Dogfish   | SSD                | 512 GB | 6       | 204   | 0     | 0.56   |
| ADATA     | SU800NS38          | 256 GB | 2       | 204   | 0     | 0.56   |
| ADATA     | SU650              | 120 GB | 37      | 257   | 37    | 0.56   |
| Innodisk  | DEM24-16GM41BC1... | 16 GB  | 2       | 202   | 0     | 0.55   |
| minisf... | SSD                | 128 GB | 4       | 201   | 0     | 0.55   |
| WDC       | WDS500G1R0A-68A4W0 | 500 GB | 5       | 200   | 0     | 0.55   |
| Samsung   | SSD 870 QVO        | 2 TB   | 14      | 199   | 0     | 0.55   |
| Transcend | TS64GMTS400SD      | 64 GB  | 11      | 198   | 0     | 0.54   |
| Kingston  | SUV500M8240G       | 240 GB | 3       | 196   | 0     | 0.54   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 17      | 196   | 0     | 0.54   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 5       | 195   | 0     | 0.54   |
| Samsung   | SSD 860 QVO        | 4 TB   | 2       | 194   | 0     | 0.53   |
| WDC       | WDS500G2B0B-00YS70 | 500 GB | 8       | 193   | 0     | 0.53   |
| Transcend | TS256GSSD452K2     | 256 GB | 6       | 193   | 0     | 0.53   |
| PNY       | CS900 240GB SSD    | 240 GB | 22      | 192   | 0     | 0.53   |
| Kingston  | SA400S37480G       | 480 GB | 39      | 195   | 1     | 0.53   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 8       | 191   | 0     | 0.53   |
| SanDisk   | SSD PLUS           | 240 GB | 28      | 229   | 3     | 0.53   |
| China     | SATA3 64GB SSD     | 64 GB  | 2       | 189   | 0     | 0.52   |
| Intel     | SSDSC2KG240G8      | 240 GB | 9       | 188   | 0     | 0.52   |
| Innodisk  | DEMSR- 08GB mSA... | 8 GB   | 15      | 188   | 0     | 0.52   |
| SATADOM   | SL 3IE3 V2         | 64 GB  | 7       | 185   | 0     | 0.51   |
| Goodram   | SSDPR-CL100-120-G2 | 120 GB | 2       | 183   | 0     | 0.50   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 3       | 214   | 74    | 0.50   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 34      | 194   | 2     | 0.50   |
| Samsung   | MZ7LH1T9HMLT0D3    | 1.9 TB | 2       | 180   | 0     | 0.50   |
| ADATA     | SU800              | 1 TB   | 3       | 344   | 15    | 0.49   |
| ADATA     | SU630              | 480 GB | 3       | 177   | 0     | 0.49   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| Dell        | 1      | 2       | 1173  | 0     | 3.22   |
| HPE         | 5      | 10      | 1135  | 0     | 3.11   |
| Mushkin     | 4      | 12      | 990   | 0     | 2.71   |
| Corsair     | 8      | 29      | 1145  | 105   | 2.56   |
| OCZ         | 17     | 61      | 1099  | 42    | 2.42   |
| Intel       | 71     | 352     | 981   | 69    | 2.07   |
| Seagate     | 8      | 16      | 679   | 0     | 1.86   |
| Samsung     | 124    | 1137    | 682   | 7     | 1.78   |
| Apple       | 8      | 24      | 674   | 6     | 1.68   |
| SuperMicro  | 2      | 6       | 612   | 0     | 1.68   |
| Toshiba     | 17     | 53      | 620   | 6     | 1.67   |
| Advantech   | 1      | 3       | 577   | 0     | 1.58   |
| TCSUNBOW    | 1      | 5       | 552   | 0     | 1.51   |
| HP          | 4      | 12      | 502   | 0     | 1.38   |
| Phison      | 5      | 64      | 500   | 0     | 1.37   |
| Hoodisk     | 6      | 199     | 462   | 0     | 1.27   |
| SanDisk     | 78     | 390     | 458   | 8     | 1.17   |
| Goodram     | 9      | 34      | 400   | 0     | 1.10   |
| MyDigita... | 1      | 4       | 658   | 2     | 1.09   |
| Crucial     | 39     | 490     | 462   | 35    | 1.08   |
| Kingston    | 50     | 744     | 457   | 20    | 1.04   |
| Micron      | 21     | 78      | 511   | 68    | 0.98   |
| PNY         | 8      | 92      | 346   | 1     | 0.94   |
| ADATA       | 27     | 170     | 359   | 31    | 0.92   |
| Smartbuy    | 2      | 4       | 335   | 0     | 0.92   |
| Patriot     | 8      | 43      | 337   | 24    | 0.92   |
| China       | 37     | 290     | 343   | 2     | 0.90   |
| Pioneer     | 1      | 2       | 322   | 0     | 0.88   |
| AMD         | 3      | 10      | 328   | 2     | 0.86   |
| SK hynix    | 14     | 49      | 418   | 20    | 0.86   |
| Innodisk    | 6      | 31      | 305   | 0     | 0.84   |
| Integral    | 1      | 3       | 295   | 0     | 0.81   |
| Apacer      | 10     | 65      | 403   | 27    | 0.81   |
| Gigabyte    | 2      | 6       | 284   | 0     | 0.78   |
| OWC         | 3      | 11      | 277   | 0     | 0.76   |
| WDC         | 24     | 253     | 268   | 4     | 0.70   |
| SPCC        | 10     | 108     | 238   | 1     | 0.64   |
| KingFast    | 8      | 47      | 255   | 21    | 0.63   |
| Wicgtyp     | 1      | 2       | 207   | 0     | 0.57   |
| Gigabyte... | 3      | 13      | 196   | 0     | 0.54   |
| Kston       | 4      | 23      | 201   | 1     | 0.52   |
| SATADOM     | 1      | 7       | 185   | 0     | 0.51   |
| Intenso     | 11     | 62      | 182   | 1     | 0.50   |
| Pccooler    | 1      | 2       | 176   | 0     | 0.48   |
| Protectli   | 9      | 63      | 168   | 0     | 0.46   |
| Team        | 3      | 7       | 165   | 0     | 0.45   |
| VICK        | 1      | 2       | 161   | 0     | 0.44   |
| BIWIN       | 2      | 30      | 186   | 9     | 0.43   |
| Transcend   | 46     | 364     | 153   | 3     | 0.42   |
| Dogfish     | 4      | 42      | 157   | 1     | 0.41   |
| KingSpec    | 11     | 34      | 153   | 1     | 0.41   |
| Zheino      | 3      | 6       | 143   | 0     | 0.39   |
| KIOXIA-E... | 2      | 4       | 142   | 0     | 0.39   |
| Vaseky      | 2      | 4       | 138   | 0     | 0.38   |
| minisforum  | 2      | 14      | 128   | 0     | 0.35   |
| ZTC         | 1      | 2       | 640   | 14    | 0.34   |
| FORESEE     | 4      | 78      | 118   | 0     | 0.33   |
| Qunion      | 1      | 2       | 126   | 1     | 0.33   |
| ORICO       | 2      | 4       | 115   | 0     | 0.32   |
| Leven       | 2      | 4       | 114   | 0     | 0.31   |
| Drevo       | 1      | 3       | 114   | 0     | 0.31   |
| Lite-On     | 11     | 27      | 112   | 75    | 0.30   |
| KingDian    | 3      | 8       | 107   | 127   | 0.29   |
| BORY        | 1      | 7       | 103   | 0     | 0.28   |
| Plextor     | 4      | 9       | 93    | 0     | 0.26   |
| Faspeed     | 1      | 4       | 90    | 0     | 0.25   |
| Verbatim    | 2      | 12      | 88    | 0     | 0.24   |
| Supermicro  | 1      | 2       | 87    | 0     | 0.24   |
| ShiJi       | 3      | 17      | 85    | 0     | 0.23   |
| UDinfo      | 1      | 3       | 82    | 0     | 0.23   |
| BAITITON    | 2      | 8       | 99    | 2     | 0.22   |
| Netac       | 5      | 13      | 73    | 1     | 0.20   |
| Lexar       | 1      | 8       | 68    | 0     | 0.19   |
| AirDisk     | 1      | 7       | 65    | 0     | 0.18   |
| KeepData    | 1      | 15      | 67    | 1     | 0.16   |
| Yeyian      | 1      | 2       | 56    | 0     | 0.15   |
| ATP         | 4      | 15      | 52    | 0     | 0.14   |
| Colorful    | 1      | 2       | 41    | 0     | 0.11   |
| XrayDisk    | 1      | 2       | 71    | 11    | 0.08   |
| SHAREVDI    | 1      | 12      | 23    | 0     | 0.06   |
| XUM         | 1      | 2       | 21    | 0     | 0.06   |
| HCiPC       | 1      | 2       | 20    | 0     | 0.06   |
| EMTEC       | 1      | 3       | 11    | 0     | 0.03   |
| SSSTC       | 2      | 5       | 8     | 605   | 0.02   |
| T-FORCE     | 1      | 2       | 6     | 0     | 0.02   |
| MEMXPRO     | 1      | 4       | 5     | 0     | 0.02   |
| Valuetech   | 1      | 2       | 5     | 0     | 0.02   |
| Fordisk     | 1      | 4       | 4     | 0     | 0.01   |
| INDMEM      | 1      | 2       | 88    | 15    | 0.01   |
| CWDISK      | 1      | 4       | 3     | 0     | 0.01   |
| VisionTek   | 1      | 3       | 1072  | 1019  | 0.00   |
| HP Phison   | 1      | 2       | 441   | 1054  | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

See top 1000 of tested NVMe models in the [Top1000_NVMe.md](/Top1000_NVMe.md).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Samsung   | SSD 950 PRO        | 512 GB | 3       | 1480  | 0     | 4.06   |
| Intel     | SSDPEDMW400G4      | 400 GB | 2       | 1410  | 0     | 3.86   |
| Intel     | SSDPE2MX450G7      | 450 GB | 2       | 1077  | 0     | 2.95   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 3       | 1053  | 0     | 2.89   |
| Intel     | SSDPED1D280GA      | 280 GB | 2       | 1036  | 0     | 2.84   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 3       | 913   | 0     | 2.50   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 2       | 804   | 0     | 2.20   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 2       | 794   | 0     | 2.18   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 2       | 765   | 0     | 2.10   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 3       | 561   | 0     | 1.54   |
| Intel     | SSDPE21D280GA      | 280 GB | 2       | 543   | 0     | 1.49   |
| HP        | SSD EX900          | 120 GB | 3       | 504   | 0     | 1.38   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 6       | 504   | 0     | 1.38   |
| Intel     | SSDPEKKW128G8      | 128 GB | 2       | 494   | 0     | 1.35   |
| Intel     | SSDPEKKW256G8      | 256 GB | 3       | 490   | 0     | 1.34   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 3       | 474   | 0     | 1.30   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 3       | 447   | 0     | 1.23   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 3       | 439   | 0     | 1.20   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 2       | 429   | 0     | 1.18   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 2       | 425   | 0     | 1.17   |
| Intel     | SSDPEKKW128G7      | 128 GB | 2       | 840   | 1     | 1.15   |
| Kingston  | SA1000M8240G       | 240 GB | 2       | 403   | 0     | 1.10   |
| Samsung   | SSD 960 EVO        | 250 GB | 23      | 400   | 0     | 1.10   |
| Corsair   | Force MP600        | 500 GB | 2       | 393   | 0     | 1.08   |
| Kingston  | SEDC1000BM8240G    | 240 GB | 3       | 390   | 0     | 1.07   |
| Corsair   | Force MP600        | 1 TB   | 2       | 388   | 0     | 1.06   |
| HP        | SSD EX920          | 512 GB | 2       | 379   | 0     | 1.04   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 3       | 378   | 0     | 1.04   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 3       | 377   | 0     | 1.03   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 5       | 375   | 0     | 1.03   |
| Samsung   | SSD 960 EVO        | 1 TB   | 3       | 407   | 1     | 1.01   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 4       | 365   | 0     | 1.00   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 3       | 364   | 0     | 1.00   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 2       | 363   | 0     | 0.99   |
| ADATA     | SX8200PNP          | 512 GB | 7       | 414   | 1     | 0.99   |
| Samsung   | SSD 970 PRO        | 512 GB | 15      | 339   | 0     | 0.93   |
| Gigaby... | GP-AG42TB          | 2 TB   | 2       | 337   | 0     | 0.93   |
| Corsair   | Force MP600        | 2 TB   | 2       | 336   | 0     | 0.92   |
| Samsung   | SSD 960 EVO        | 500 GB | 11      | 333   | 0     | 0.91   |
| Silico... | 512GB PCS PCIe ... | 512 GB | 2       | 333   | 0     | 0.91   |
| Phison    | PCIe SSD           | 500 GB | 8       | 333   | 0     | 0.91   |
| Phison    | Sabrent            | 1 TB   | 19      | 325   | 0     | 0.89   |
| ADATA     | SX6000NP           | 128 GB | 2       | 325   | 0     | 0.89   |
| ADATA     | SX8200PNP          | 1 TB   | 11      | 334   | 5     | 0.88   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 2       | 311   | 0     | 0.85   |
| Kingston  | SA2000M81000G      | 1 TB   | 7       | 314   | 145   | 0.83   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 2       | 297   | 0     | 0.81   |
| Crucial   | CT500P1SSD8        | 500 GB | 8       | 289   | 0     | 0.79   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 9       | 285   | 0     | 0.78   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 2       | 279   | 0     | 0.77   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 4       | 278   | 0     | 0.76   |
| Micron    | 7300_MTFDHBA400TDG | 400 GB | 2       | 272   | 0     | 0.75   |
| Samsung   | SSD 970 PRO        | 1 TB   | 8       | 271   | 0     | 0.74   |
| Samsung   | SSD 970 EVO        | 250 GB | 14      | 270   | 0     | 0.74   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 15      | 267   | 0     | 0.73   |
| KIOXIA... | SSD                | 500 GB | 3       | 263   | 0     | 0.72   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 3       | 263   | 0     | 0.72   |
| Intel     | SSDPEKNW512G8      | 512 GB | 11      | 262   | 0     | 0.72   |
| WDC       | WDS100T1X0E-00AFY0 | 1 TB   | 5       | 260   | 0     | 0.71   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 3       | 249   | 0     | 0.68   |
| minisf... | 512GB              | 512 GB | 2       | 246   | 0     | 0.68   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 2       | 240   | 0     | 0.66   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 7       | 239   | 0     | 0.66   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 2       | 236   | 0     | 0.65   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 31      | 234   | 0     | 0.64   |
| Samsung   | MZVLW256HEHP-00000 | 256 GB | 2       | 234   | 0     | 0.64   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 14      | 234   | 0     | 0.64   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 4       | 230   | 0     | 0.63   |
| Seagate   | BarraCuda Q5 ZP... | 500 GB | 2       | 227   | 0     | 0.62   |
| Kingston  | SA2000M8500G       | 500 GB | 10      | 225   | 0     | 0.62   |
| WDC       | WDS500G1X0E-00AFY0 | 500 GB | 3       | 224   | 0     | 0.61   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 12      | 218   | 0     | 0.60   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 3       | 218   | 0     | 0.60   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 2       | 216   | 0     | 0.59   |
| Transcend | TS500GMTE240S      | 500 GB | 2       | 214   | 0     | 0.59   |
| PNY       | CS3030 500GB SSD   | 500 GB | 3       | 212   | 0     | 0.58   |
| Corsair   | Force MP510        | 240 GB | 4       | 209   | 0     | 0.57   |
| ADATA     | SX8200PNP          | 256 GB | 6       | 207   | 0     | 0.57   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 2       | 203   | 0     | 0.56   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 3       | 200   | 0     | 0.55   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 12      | 200   | 0     | 0.55   |
| Crucial   | CT500P5PSSD8       | 500 GB | 2       | 199   | 0     | 0.55   |
| Micron    | 2200S NVMe         | 256 GB | 3       | 198   | 0     | 0.54   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 6       | 195   | 0     | 0.53   |
| WDC       | PC SN730 NVMe      | 1 TB   | 2       | 194   | 0     | 0.53   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 2       | 193   | 0     | 0.53   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 6       | 192   | 0     | 0.53   |
| Intel     | HBRPEKNX0101AH     | 256 GB | 2       | 192   | 0     | 0.53   |
| Silico... | 512GB              | 512 GB | 2       | 188   | 0     | 0.52   |
| SSSTC     | CL1-4D256          | 256 GB | 2       | 182   | 0     | 0.50   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 8       | 210   | 1     | 0.49   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 4       | 177   | 0     | 0.49   |
| Transcend | TS128GMTE110S      | 128 GB | 15      | 176   | 0     | 0.48   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 13      | 184   | 15    | 0.47   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 3       | 167   | 0     | 0.46   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 9       | 166   | 0     | 0.46   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 2       | 165   | 0     | 0.45   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 2       | 164   | 0     | 0.45   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 7       | 164   | 0     | 0.45   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 5       | 160   | 0     | 0.44   |
| Samsung   | SSD 970 EVO        | 500 GB | 23      | 178   | 1     | 0.44   |
| Goodram   | SSDPR-PX500-256-80 | 256 GB | 3       | 160   | 0     | 0.44   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 2       | 154   | 0     | 0.42   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 2       | 154   | 0     | 0.42   |
| Samsung   | PM951 NVMe         | 256 GB | 4       | 153   | 0     | 0.42   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 3       | 152   | 0     | 0.42   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 7       | 151   | 0     | 0.41   |
| Gigabyte  | GP-GSM2NE3256GNTD  |        | 6       | 150   | 0     | 0.41   |
| Toshiba   | KXG6AZNV256G       | 256 GB | 2       | 150   | 0     | 0.41   |
| UMIS      | RPJTJ256MEE1OWX    | 256 GB | 2       | 147   | 0     | 0.41   |
| SK hynix  | SHGP31-500GM-2     | 500 GB | 5       | 147   | 0     | 0.41   |
| Toshiba   | KBG40ZNT512G ME... | 512 GB | 2       | 147   | 0     | 0.40   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 42      | 147   | 0     | 0.40   |
| SK hynix  | BC511 NVMe         | 256 GB | 2       | 146   | 0     | 0.40   |
| Samsung   | SSD 970 EVO        | 1 TB   | 16      | 145   | 0     | 0.40   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 7       | 145   | 0     | 0.40   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 4       | 144   | 0     | 0.39   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 10      | 143   | 0     | 0.39   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 2       | 142   | 0     | 0.39   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 4       | 141   | 0     | 0.39   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 6       | 141   | 0     | 0.39   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 2       | 140   | 0     | 0.39   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 38      | 139   | 0     | 0.38   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 10      | 138   | 0     | 0.38   |
| Gigabyte  | GP-GSM2NE3128GNTD  | 128 GB | 3       | 137   | 0     | 0.38   |
| WDC       | PC SN520 NVMe      | 256 GB | 2       | 136   | 0     | 0.37   |
| Silico... | NE-256             | 256 GB | 5       | 135   | 0     | 0.37   |
| LDLC      | F8+M.2 240         | 240 GB | 2       | 134   | 0     | 0.37   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 5       | 132   | 0     | 0.36   |
| WDC       | WDBRPG0010BNC-WRSN | 1 TB   | 2       | 131   | 0     | 0.36   |
| Kingston  | SA2000M8250G       | 250 GB | 12      | 131   | 0     | 0.36   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 11      | 128   | 0     | 0.35   |
| Lexar     | 256GB SSD          | 256 GB | 6       | 127   | 0     | 0.35   |
| Samsung   | PM981 NVMe         | 256 GB | 4       | 127   | 0     | 0.35   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 11      | 127   | 0     | 0.35   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 2       | 127   | 0     | 0.35   |
| Team      | TM8FP6512G         | 512 GB | 2       | 124   | 0     | 0.34   |
| Corsair   | Force MP510        | 480 GB | 4       | 122   | 0     | 0.34   |
| SanDisk   | WD Blue SN570      | 250 GB | 4       | 119   | 0     | 0.33   |
| Samsung   | SSD 980 PRO        | 250 GB | 9       | 118   | 0     | 0.33   |
| SanDisk   | WD_BLACK SN770     | 1 TB   | 2       | 118   | 0     | 0.32   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 2       | 116   | 0     | 0.32   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 9       | 115   | 0     | 0.32   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 5       | 115   | 0     | 0.32   |
| Micron    | 2300_MTFDHBA512TDV | 512 GB | 2       | 113   | 0     | 0.31   |
| Kingston  | OM8PDP3512B-A01    | 512 GB | 9       | 112   | 0     | 0.31   |
| Samsung   | SSD 960 PRO        | 512 GB | 4       | 226   | 1     | 0.30   |
| Kingston  | OM8PCP3512F-AI1    | 512 GB | 2       | 110   | 0     | 0.30   |
| Samsung   | SSD 980            | 250 GB | 8       | 110   | 0     | 0.30   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 10      | 110   | 0     | 0.30   |
| Intel     | SSDPEKKW512G7      | 512 GB | 2       | 174   | 1     | 0.30   |
| Fanxiang  | S501               | 512 GB | 3       | 106   | 0     | 0.29   |
| Samsung   | SSD 970 EVO        | 2 TB   | 2       | 364   | 130   | 0.28   |
| Seagate   | FireCuda 520 SS... | 500 GB | 6       | 103   | 0     | 0.28   |
| KIOXIA    | KBG40ZNS128G NVMe  | 128 GB | 3       | 102   | 0     | 0.28   |
| Samsung   | PM991 NVMe         | 256 GB | 5       | 102   | 0     | 0.28   |
| HP        | SSD EX950          | 512 GB | 10      | 102   | 0     | 0.28   |
| SK hynix  | BC511 HFM256GDJ... | 256 GB | 5       | 99    | 0     | 0.27   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 6       | 98    | 0     | 0.27   |
| Kingston  | RBUSNS8154P3256GJ3 | 256 GB | 2       | 98    | 0     | 0.27   |
| Crucial   | CT2000P2SSD8       | 2 TB   | 3       | 97    | 0     | 0.27   |
| Kingston  | SA1000M8480G       | 480 GB | 2       | 94    | 0     | 0.26   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 4       | 94    | 0     | 0.26   |
| Micron    | 2200S NVMe         | 1 TB   | 3       | 92    | 0     | 0.25   |
| ADATA     | SX6000LNP          | 128 GB | 2       | 92    | 0     | 0.25   |
| Transcend | TS2TMTE220S        | 2 TB   | 2       | 90    | 0     | 0.25   |
| Samsung   | MZALQ128HBHQ-000L1 | 128 GB | 6       | 89    | 0     | 0.25   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 2       | 89    | 0     | 0.24   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 6       | 87    | 0     | 0.24   |
| Samsung   | MZVLB512HBJQ-000H1 | 512 GB | 3       | 85    | 0     | 0.23   |
| SK hynix  | SHGP31-1000GM      | 1 TB   | 2       | 81    | 0     | 0.22   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 7       | 78    | 0     | 0.21   |
| ATP       | NVMe M.2 2280 SSD  | 240 GB | 6       | 75    | 0     | 0.21   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 2       | 74    | 0     | 0.20   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 2       | 74    | 0     | 0.20   |
| Crucial   | CT500P2SSD8        | 500 GB | 13      | 73    | 0     | 0.20   |
| Samsung   | MZALQ256HBJD-00BL2 | 256 GB | 2       | 72    | 0     | 0.20   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 3       | 71    | 0     | 0.20   |
| Micron    | 2210_MTFDHBA512QFD | 512 GB | 2       | 71    | 0     | 0.19   |
| Kingston  | SNVS1000G          | 1 TB   | 2       | 70    | 0     | 0.19   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 5       | 69    | 0     | 0.19   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 2       | 69    | 0     | 0.19   |
| Kingston  | OM8PDP3256B-A01    | 256 GB | 6       | 68    | 0     | 0.19   |
| Lenovo    | LENSE30512GMSP3... | 512 GB | 2       | 67    | 0     | 0.18   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 2       | 66    | 0     | 0.18   |
| KIOXIA    | KXG60ZNV256G       | 256 GB | 2       | 66    | 0     | 0.18   |
| BIWIN     | SSD                | 1 TB   | 3       | 66    | 0     | 0.18   |
| Samsung   | PM961 NVMe         | 256 GB | 2       | 65    | 0     | 0.18   |
| Samsung   | MZVLQ256HAJD-000H1 | 256 GB | 4       | 63    | 0     | 0.17   |
| ORTIAL    | SSD                | 128 GB | 2       | 62    | 0     | 0.17   |
| Silico... | 128GB              | 128 GB | 3       | 61    | 0     | 0.17   |
| Kimtigo   | SSD                | 128 GB | 2       | 60    | 0     | 0.16   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 2       | 58    | 0     | 0.16   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 11      | 58    | 0     | 0.16   |
| Lexar     | SSD                | 256 GB | 2       | 57    | 0     | 0.16   |
| Crucial   | CT500P5SSD8        | 500 GB | 4       | 57    | 0     | 0.16   |
| SanDisk   | Ultra 3D NVMe      | 500 GB | 2       | 57    | 0     | 0.16   |
| Samsung   | MZALQ512HALU-000L2 | 512 GB | 2       | 54    | 0     | 0.15   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 3       | 54    | 0     | 0.15   |
| SanDisk   | WD Blue SN570      | 500 GB | 11      | 52    | 0     | 0.14   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 4       | 51    | 0     | 0.14   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 3       | 50    | 0     | 0.14   |
| Kingston  | SNVS250G           | 250 GB | 6       | 49    | 0     | 0.14   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 3       | 49    | 0     | 0.14   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 3       | 49    | 0     | 0.14   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 7       | 49    | 0     | 0.14   |
| Samsung   | SSD 980 PRO        | 500 GB | 21      | 47    | 0     | 0.13   |
| Star D... | PCIe SSD           | 960 GB | 3       | 47    | 0     | 0.13   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 4       | 47    | 0     | 0.13   |
| Union ... | UMIS LENSE40256... | 256 GB | 2       | 47    | 0     | 0.13   |
| Crucial   | CT250P2SSD8        | 250 GB | 14      | 46    | 0     | 0.13   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 3       | 44    | 0     | 0.12   |
| SK hynix  | BC711 NVMe         | 256 GB | 2       | 44    | 0     | 0.12   |
| Micron    | 2200S NVMe         | 512 GB | 3       | 43    | 0     | 0.12   |
| Kingston  | SNVS500G           | 500 GB | 8       | 41    | 0     | 0.11   |
| PNY       | CS1030 250GB SSD   | 250 GB | 2       | 40    | 0     | 0.11   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 2       | 39    | 0     | 0.11   |
| Kingston  | OM8PCP3512F-AA     | 512 GB | 2       | 39    | 0     | 0.11   |
| Samsung   | SSD 980            | 500 GB | 20      | 49    | 2     | 0.11   |
| Samsung   | SSD 980 PRO        | 1 TB   | 26      | 39    | 0     | 0.11   |
| Colorful  | CN600              | 512 GB | 2       | 38    | 0     | 0.10   |
| Micron    | MTFDHBA512QFD-1... | 512 GB | 2       | 37    | 0     | 0.10   |
| Samsung   | SSD 980            | 1 TB   | 18      | 37    | 0     | 0.10   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 2       | 36    | 0     | 0.10   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 4       | 36    | 0     | 0.10   |
| HP        | SSD EX900          | 500 GB | 2       | 35    | 0     | 0.10   |
| Samsung   | PM9A1 NVMe         | 512 GB | 5       | 33    | 0     | 0.09   |
| Lite-On   | CA3-8D512          | 512 GB | 2       | 33    | 0     | 0.09   |
| Transcend | TS256GMTE652T2     | 256 GB | 17      | 32    | 0     | 0.09   |
| Samsung   | MZVL2512HCJQ-00B00 | 512 GB | 2       | 32    | 0     | 0.09   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 7       | 32    | 0     | 0.09   |
| Kingston  | OM8PDP3256B-AI1    | 256 GB | 4       | 32    | 0     | 0.09   |
| SanDisk   | WD_BLACK SN770     | 500 GB | 6       | 32    | 0     | 0.09   |
| Kingston  | RBUSNS8154P3256GJ1 | 256 GB | 3       | 30    | 0     | 0.08   |
| ADATA     | SX6000PNP          | 512 GB | 2       | 29    | 0     | 0.08   |
| Gigaby... | GP-GSM2NE3256GNTD  | 256 GB | 3       | 29    | 0     | 0.08   |
| Phison    | minisforum         | 512 GB | 2       | 28    | 0     | 0.08   |
| SanDisk   | WD_BLACK SN770     | 250 GB | 3       | 28    | 0     | 0.08   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 2       | 27    | 0     | 0.07   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 5       | 26    | 0     | 0.07   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 3       | 24    | 0     | 0.07   |
| Fanxiang  | S500               | 256 GB | 2       | 23    | 0     | 0.06   |
| Gigaby... | GP-GSM2NE3100TNTD  | 1 TB   | 2       | 22    | 0     | 0.06   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 5       | 22    | 0     | 0.06   |
| Kingston  | SNV2S250G          | 250 GB | 3       | 22    | 0     | 0.06   |
| SanDisk   | WD Green SN350     | 2 TB   | 2       | 22    | 0     | 0.06   |
| HGST      | HUSMR7632BDP301    |        | 2       | 22    | 0     | 0.06   |
| Kingston  | SKC2500M8250G      | 250 GB | 2       | 22    | 0     | 0.06   |
| Fanxiang  | S500               | 128 GB | 6       | 21    | 0     | 0.06   |
| Mushkin   | MKNSSDHL1TB-D8     | 1 TB   | 2       | 21    | 0     | 0.06   |
| Crucial   | CT500P3SSD8        | 500 GB | 5       | 21    | 0     | 0.06   |
| Micron    | 2300 NVMe          | 512 GB | 3       | 21    | 0     | 0.06   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 2       | 20    | 0     | 0.06   |
| Patriot   | M.2 P300           | 256 GB | 4       | 20    | 0     | 0.05   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 2       | 19    | 0     | 0.05   |
| Team      | TM8FP6256G         | 256 GB | 5       | 19    | 0     | 0.05   |
| Micron    | 7450_MTFDKBA800TFS |        | 2       | 19    | 0     | 0.05   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 4       | 17    | 0     | 0.05   |
| Fanxiang  | S500PRO            | 256 GB | 8       | 17    | 0     | 0.05   |
| SanDisk   | WD Blue SN570      | 1 TB   | 7       | 17    | 0     | 0.05   |
| Micron    | 2450_MTFDKBA1T0TFK | 1 TB   | 2       | 17    | 0     | 0.05   |
| SK hynix  | BC511 NVMe         | 512 GB | 3       | 15    | 0     | 0.04   |
| FORESEE   | XP1000F001T        | 1 TB   | 4       | 15    | 0     | 0.04   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 2       | 14    | 0     | 0.04   |
| Samsung   | MZVL2512HCJQ-00B07 | 512 GB | 4       | 14    | 0     | 0.04   |
| ADATA     | SX6000PNP          | 256 GB | 2       | 13    | 0     | 0.04   |
| AGI       | AGI512G16AI198     | 512 GB | 2       | 33    | 1     | 0.03   |
| ADATA     | SX6000LNP          | 512 GB | 3       | 11    | 0     | 0.03   |
| Intel     | SSDPEKNU512GZ      | 512 GB | 4       | 11    | 0     | 0.03   |
| Crucial   | CT2000P3SSD8       | 2 TB   | 2       | 11    | 0     | 0.03   |
| Kingston  | OM8PDP3256B-AA1    | 256 GB | 2       | 11    | 0     | 0.03   |
| Kingston  | SFYRS1000G         | 1 TB   | 2       | 10    | 0     | 0.03   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 2       | 10    | 0     | 0.03   |
| SPCC      | M.2 PCIe SSD       | 128 GB | 4       | 9     | 0     | 0.03   |
| Samsung   | MZALQ256HAJD-000L2 | 256 GB | 3       | 9     | 0     | 0.03   |
| Mushkin   | MKNSSDHL500GB-D8   | 500 GB | 2       | 8     | 0     | 0.02   |
| SanDisk   | WD_BLACK SN850     | 1 TB   | 2       | 7     | 0     | 0.02   |
| WDC       | PC SN530 NVMe      | 256 GB | 3       | 7     | 0     | 0.02   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 3       | 6     | 0     | 0.02   |
| Kingston  | SKC3000S1024G      | 1 TB   | 4       | 6     | 0     | 0.02   |
| Phison    | Sabrent SB-1342... | 512 GB | 2       | 6     | 0     | 0.02   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 2       | 6     | 0     | 0.02   |
| Fanxiang  | S501               | 128 GB | 7       | 6     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 2       | 5     | 0     | 0.02   |
| Samsung   | MZALQ512HBLU-00BL2 | 512 GB | 3       | 4     | 0     | 0.01   |
| Samsung   | SSD 980 PRO        | 2 TB   | 6       | 4     | 0     | 0.01   |
| Samsung   | MZALQ512HBLU-00BL1 | 512 GB | 4       | 3     | 0     | 0.01   |
| Silico... | NS256GSSD530       | 256 GB | 3       | 3     | 0     | 0.01   |
| Team      | TM8FPD512G         | 512 GB | 2       | 3     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 2       | 3     | 0     | 0.01   |
| Samsung   | MZVL21T0HCLR-00BL7 | 1 TB   | 3       | 3     | 0     | 0.01   |
| Silico... | GV128              | 128 GB | 6       | 2     | 0     | 0.01   |
| Kingston  | SNV2S500G          | 500 GB | 5       | 2     | 0     | 0.01   |
| Silico... | 256GB              | 256 GB | 2       | 1     | 0     | 0.00   |
| ShiJi     | 256GB M.2-NVMe     | 256 GB | 2       | 1     | 0     | 0.00   |
| SK hynix  | SHGP31-500GM       | 500 GB | 2       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 3       | 0     | 0     | 0.00   |
| Transcend | TS256GMTE710T      | 256 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | MZALQ256HAJD-000L1 | 256 GB | 2       | 0     | 0     | 0.00   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| Toshiba     | 11     | 29      | 333   | 0     | 0.91   |
| Phison      | 6      | 42      | 300   | 0     | 0.82   |
| Intel       | 23     | 89      | 286   | 1     | 0.75   |
| KIOXIA-E... | 1      | 3       | 263   | 0     | 0.72   |
| Corsair     | 5      | 14      | 254   | 0     | 0.70   |
| minisforum  | 1      | 2       | 246   | 0     | 0.68   |
| ADATA       | 8      | 35      | 251   | 2     | 0.65   |
| WDC         | 37     | 162     | 204   | 0     | 0.56   |
| HP          | 4      | 17      | 197   | 0     | 0.54   |
| SSSTC       | 2      | 5       | 173   | 0     | 0.48   |
| PNY         | 3      | 8       | 164   | 0     | 0.45   |
| Goodram     | 1      | 3       | 160   | 0     | 0.44   |
| Samsung     | 69     | 539     | 162   | 1     | 0.44   |
| Lenovo      | 2      | 4       | 152   | 0     | 0.42   |
| KIOXIA      | 5      | 20      | 149   | 0     | 0.41   |
| UMIS        | 1      | 2       | 147   | 0     | 0.41   |
| Gigabyte    | 2      | 9       | 146   | 0     | 0.40   |
| XPG         | 1      | 6       | 141   | 0     | 0.39   |
| LDLC        | 1      | 2       | 134   | 0     | 0.37   |
| Seagate     | 2      | 8       | 134   | 0     | 0.37   |
| Kingston    | 25     | 104     | 117   | 10    | 0.32   |
| Gigabyte... | 3      | 7       | 115   | 0     | 0.32   |
| Lexar       | 2      | 8       | 110   | 0     | 0.30   |
| Crucial     | 11     | 81      | 111   | 3     | 0.30   |
| Transcend   | 5      | 38      | 100   | 0     | 0.27   |
| SPCC        | 4      | 19      | 98    | 0     | 0.27   |
| Micron      | 12     | 29      | 92    | 0     | 0.25   |
| Silicon ... | 7      | 23      | 84    | 0     | 0.23   |
| ATP         | 1      | 6       | 75    | 0     | 0.21   |
| SK hynix    | 13     | 38      | 69    | 0     | 0.19   |
| BIWIN       | 1      | 3       | 66    | 0     | 0.18   |
| ORTIAL      | 1      | 2       | 62    | 0     | 0.17   |
| Kimtigo     | 1      | 2       | 60    | 0     | 0.16   |
| SanDisk     | 9      | 39      | 47    | 0     | 0.13   |
| Star Drive  | 1      | 3       | 47    | 0     | 0.13   |
| Union Me... | 1      | 2       | 47    | 0     | 0.13   |
| Team        | 3      | 9       | 39    | 0     | 0.11   |
| Colorful    | 1      | 2       | 38    | 0     | 0.10   |
| Lite-On     | 1      | 2       | 33    | 0     | 0.09   |
| Fanxiang    | 5      | 26      | 26    | 0     | 0.07   |
| HGST        | 1      | 2       | 22    | 0     | 0.06   |
| Patriot     | 1      | 4       | 20    | 0     | 0.05   |
| FORESEE     | 1      | 4       | 15    | 0     | 0.04   |
| Mushkin     | 2      | 4       | 15    | 0     | 0.04   |
| AGI         | 1      | 2       | 33    | 1     | 0.03   |
| ShiJi       | 1      | 2       | 1     | 0     | 0.00   |

