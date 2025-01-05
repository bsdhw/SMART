HDD/SSD Reliability Test
------------------------

This is a project to estimate reliability of HDD/SSD drives by
the analysis of SMART data collected by BSD users at https://bsd-hardware.info. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe/blob/master/INSTALL.BSD.md) tool:

    hw-probe -all -upload

Total drives: 20793.

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
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 2       | 3820  | 0     | 10.47  |
| Hitachi   | HDS725050KLA360    | 500 GB | 4       | 3436  | 0     | 9.41   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 5       | 4337  | 2     | 9.40   |
| WDC       | WD5002ABYS-50B1B1  | 500 GB | 2       | 3336  | 0     | 9.14   |
| Toshiba   | MG03ACA300         | 3 TB   | 2       | 3316  | 0     | 9.08   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 6       | 3085  | 0     | 8.45   |
| WDC       | WD1602ABKS-18N8A0  | 160 GB | 2       | 3022  | 0     | 8.28   |
| Seagate   | ST3500630AS        | 500 GB | 3       | 3022  | 0     | 8.28   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 2       | 2975  | 0     | 8.15   |
| Seagate   | ST3808110AS        | 80 GB  | 2       | 2844  | 0     | 7.79   |
| Seagate   | ST3500630NS        | 500 GB | 5       | 2830  | 0     | 7.75   |
| Hitachi   | HUA7250SBSUN500G   | 500 GB | 2       | 2785  | 0     | 7.63   |
| Samsung   | HD321HJ            | 320 GB | 2       | 2759  | 0     | 7.56   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 4       | 2729  | 0     | 7.48   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 2       | 2628  | 0     | 7.20   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 3       | 3475  | 11    | 7.19   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 3       | 3406  | 1     | 7.13   |
| Hitachi   | HUA721050KLA330    | 500 GB | 2       | 3842  | 1     | 7.02   |
| HGST      | HUS724020ALA640    | 2 TB   | 11      | 2551  | 0     | 6.99   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 6       | 3224  | 1     | 6.98   |
| Samsung   | HD502IJ            | 500 GB | 2       | 2696  | 1     | 6.93   |
| Seagate   | ST1500DL003-9VT16L | 1.5 TB | 2       | 2521  | 0     | 6.91   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 4       | 2488  | 0     | 6.82   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 5       | 2859  | 2     | 6.75   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 10      | 2452  | 0     | 6.72   |
| Seagate   | ST32000641AS       | 2 TB   | 5       | 2443  | 0     | 6.69   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 7       | 3254  | 2     | 6.62   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 9       | 2463  | 1     | 6.61   |
| HP        | GB0250EAFYK        | 250 GB | 3       | 3054  | 1     | 6.61   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 9       | 2601  | 1     | 6.58   |
| WDC       | WD1600AAJS-00Z4A0  | 160 GB | 2       | 2386  | 0     | 6.54   |
| WDC       | WD5001AALS-00L3B2  | 500 GB | 3       | 2374  | 0     | 6.51   |
| Seagate   | ST380011A          | 80 GB  | 2       | 2353  | 0     | 6.45   |
| WDC       | WD800JD-08MSA1     | 80 GB  | 3       | 3029  | 170   | 6.41   |
| WDC       | WD1003FBYX-23 0... | 1 TB   | 2       | 2317  | 0     | 6.35   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 2       | 2316  | 0     | 6.35   |
| WDC       | WD5002ABYS-18B1B0  | 500 GB | 3       | 2886  | 3     | 6.35   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 7       | 2509  | 1     | 6.33   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 5       | 2305  | 0     | 6.32   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 3       | 2236  | 0     | 6.13   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 9       | 2206  | 0     | 6.05   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 7       | 2797  | 3     | 5.95   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 2168  | 0     | 5.94   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 3       | 3312  | 2     | 5.89   |
| HGST      | HDN724040ALE640    | 4 TB   | 41      | 2322  | 69    | 5.88   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 27      | 2494  | 1     | 5.84   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 3       | 2101  | 0     | 5.76   |
| HP        | GB0500EAFYL        | 500 GB | 4       | 2079  | 0     | 5.70   |
| Hitachi   | HDS5C4040ALE630    | 4 TB   | 21      | 2076  | 0     | 5.69   |
| WDC       | WD3200BEKT-08PVMT1 | 320 GB | 5       | 2075  | 0     | 5.69   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 4       | 2069  | 0     | 5.67   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 2       | 2045  | 0     | 5.60   |
| HGST      | HDN724030ALE640    | 3 TB   | 9       | 2037  | 0     | 5.58   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 7       | 2030  | 0     | 5.56   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 2       | 2009  | 0     | 5.51   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 2       | 2004  | 0     | 5.49   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 15      | 2650  | 51    | 5.48   |
| Seagate   | ST3320413AS        | 320 GB | 3       | 1994  | 0     | 5.46   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 7       | 1993  | 0     | 5.46   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 5       | 3192  | 3     | 5.46   |
| WDC       | WD2500AAKX-753CA1  | 250 GB | 5       | 1988  | 0     | 5.45   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 7       | 2136  | 145   | 5.37   |
| Seagate   | ST32000645NS       | 2 TB   | 2       | 1938  | 0     | 5.31   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 2       | 1916  | 0     | 5.25   |
| HP        | MB1000GCEEK        | 1 TB   | 4       | 1910  | 0     | 5.23   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 18      | 2020  | 2     | 5.23   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 2       | 1906  | 0     | 5.22   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 2       | 2003  | 3     | 5.10   |
| HGST      | HTE721010A9E630    | 1 TB   | 3       | 1849  | 0     | 5.07   |
| WDC       | WD2503ABYZ-011FA0  | 256 GB | 3       | 1809  | 0     | 4.96   |
| Toshiba   | MG03ACA200         | 2 TB   | 6       | 1760  | 0     | 4.82   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 4       | 1752  | 0     | 4.80   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 12      | 1972  | 3     | 4.77   |
| Hitachi   | HDE721064SLA360    | 640 GB | 2       | 2764  | 6     | 4.77   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 33      | 1795  | 32    | 4.77   |
| Seagate   | ST6000DX000-1H217Z | 6 TB   | 2       | 1714  | 0     | 4.70   |
| Hitachi   | HDT725025VLA380    | 250 GB | 5       | 1697  | 0     | 4.65   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 15      | 1951  | 135   | 4.64   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 3       | 2082  | 1     | 4.60   |
| HPE       | MB4000GCWLV        | 4 TB   | 9       | 1662  | 0     | 4.55   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 16      | 1960  | 80    | 4.54   |
| Samsung   | HD204UI            | 2 TB   | 28      | 2239  | 5     | 4.52   |
| Seagate   | ST2000VM003-1CT164 | 2 TB   | 2       | 1648  | 0     | 4.52   |
| Toshiba   | MG04ACA100N        | 1 TB   | 2       | 1644  | 0     | 4.51   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 4       | 2898  | 3     | 4.50   |
| Toshiba   | MG04ACA400E        | 4 TB   | 2       | 1635  | 0     | 4.48   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 5       | 1998  | 1     | 4.47   |
| WDC       | WD2005FBYZ-01YCBB1 | 2 TB   | 2       | 1626  | 0     | 4.46   |
| Seagate   | ST320011A          | 20 GB  | 2       | 1616  | 0     | 4.43   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 2       | 1611  | 0     | 4.42   |
| Seagate   | ST3500414CS        | 500 GB | 7       | 1610  | 5     | 4.41   |
| Samsung   | HE103UJ            | 1 TB   | 2       | 2313  | 130   | 4.39   |
| Seagate   | ST3300831AS        | 304 GB | 2       | 2192  | 1059  | 4.37   |
| Hitachi   | HDT725032VLA360    | 320 GB | 3       | 2689  | 2     | 4.36   |
| Hitachi   | HUA721075KLA330    | 752 GB | 2       | 1592  | 0     | 4.36   |
| Seagate   | ST3360320AS        | 360 GB | 2       | 1679  | 3     | 4.33   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 10      | 2241  | 206   | 4.28   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 8       | 1557  | 0     | 4.27   |
| WDC       | WD20NMVW-11EDZS2   | 2 TB   | 2       | 1545  | 0     | 4.23   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 3       | 1544  | 0     | 4.23   |
| WDC       | WD10PURX-64E5EY0   | 1 TB   | 2       | 1771  | 1     | 4.22   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 2       | 2615  | 545   | 4.22   |
| HP        | VB0250EAVER        | 250 GB | 7       | 2264  | 2     | 4.15   |
| Maxtor    | 6L080J4            | 80 GB  | 3       | 2093  | 2     | 4.15   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 14      | 1508  | 0     | 4.13   |
| Hitachi   | HDP725050GLA360    | 500 GB | 4       | 1794  | 10    | 4.13   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 2       | 1504  | 0     | 4.12   |
| HP        | MB1000GCWCV        | 1 TB   | 7       | 2011  | 4     | 4.09   |
| Hitachi   | HTE543232A7A384    | 320 GB | 4       | 1848  | 10    | 4.08   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 17      | 2164  | 155   | 4.06   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 4       | 1560  | 1     | 4.05   |
| WDC       | WD2500JS-75NCB2    | 250 GB | 4       | 1473  | 0     | 4.04   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 7       | 1471  | 0     | 4.03   |
| WDC       | WD2000FYYX         | 2 TB   | 4       | 1466  | 0     | 4.02   |
| Seagate   | ST9500620NS        | 500 GB | 4       | 2159  | 19    | 4.01   |
| Toshiba   | MK2565GSX          | 250 GB | 4       | 1504  | 5     | 4.00   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 2       | 1460  | 0     | 4.00   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 7       | 1808  | 1     | 3.99   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 2       | 1450  | 0     | 3.97   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 2       | 1449  | 0     | 3.97   |
| WDC       | WD3200AAKX-001CA0  | 320 GB | 3       | 2608  | 4     | 3.96   |
| Hitachi   | HDS728080PLA380    | 82 GB  | 4       | 1438  | 0     | 3.94   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 47      | 1742  | 1     | 3.93   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 16      | 2338  | 138   | 3.92   |
| Seagate   | ST4000NC000-1FR168 | 4 TB   | 3       | 1422  | 0     | 3.90   |
| Hitachi   | HDS721075KLA330    | 752 GB | 9       | 1767  | 1     | 3.90   |
| WDC       | WD6400AAKS-65A7B2  | 640 GB | 2       | 2389  | 4     | 3.89   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 12      | 1416  | 0     | 3.88   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 4       | 1411  | 0     | 3.87   |
| WDC       | WD20NPVZ-00WFZT0   | 2 TB   | 2       | 1409  | 0     | 3.86   |
| Samsung   | HD502HI            | 500 GB | 2       | 1402  | 0     | 3.84   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 4       | 1386  | 0     | 3.80   |
| WDC       | WD3201ABYS-01B9A0  | 320 GB | 2       | 1384  | 0     | 3.79   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 5       | 1373  | 0     | 3.76   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 40      | 1951  | 49    | 3.76   |
| Seagate   | ST3250823AS        | 250 GB | 2       | 2539  | 4     | 3.72   |
| WDC       | WD5000LPLX-22ZNTT0 | 500 GB | 5       | 2154  | 94    | 3.71   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 4       | 1797  | 28    | 3.71   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 5       | 2065  | 2     | 3.70   |
| Toshiba   | DT01ACA300         | 3 TB   | 21      | 1510  | 50    | 3.67   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 6       | 1336  | 0     | 3.66   |
| Samsung   | HD103SJ            | 1 TB   | 11      | 1791  | 185   | 3.66   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 7       | 1330  | 0     | 3.64   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 5       | 1796  | 2     | 3.63   |
| HGST      | HUH721212ALE601    | 12 TB  | 14      | 1405  | 1     | 3.63   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 2       | 1322  | 0     | 3.62   |
| Toshiba   | MK2561GSYB         | 250 GB | 2       | 1306  | 0     | 3.58   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 4       | 1301  | 0     | 3.57   |
| Seagate   | ST33000651AS       | 3 TB   | 2       | 1296  | 0     | 3.55   |
| HGST      | HTE725032A7E630    | 320 GB | 11      | 1446  | 6     | 3.55   |
| WDC       | WD5000BEVT-22ZAT0  | 500 GB | 4       | 1288  | 0     | 3.53   |
| HGST      | HDN726040ALE614    | 4 TB   | 15      | 1509  | 2     | 3.51   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 76      | 1597  | 2     | 3.50   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 17      | 1489  | 2     | 3.48   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 2       | 1268  | 0     | 3.48   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 14      | 1342  | 1     | 3.47   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 6       | 1467  | 2     | 3.46   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 2       | 1260  | 0     | 3.45   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 2       | 1254  | 0     | 3.44   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 3       | 1243  | 0     | 3.41   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 3       | 1375  | 3     | 3.37   |
| Seagate   | ST3160812AS        | 160 GB | 8       | 1674  | 168   | 3.37   |
| Toshiba   | MK2002TSKB         | 2 TB   | 3       | 1524  | 2     | 3.33   |
| HP        | FB160C4081         | 160 GB | 3       | 3197  | 3     | 3.32   |
| Maxtor    | 6V080E0            | 80 GB  | 2       | 1262  | 1     | 3.32   |
| Seagate   | ST380815AS         | 80 GB  | 16      | 1691  | 346   | 3.30   |
| WDC       | WD1600BEVT-22A23T0 | 160 GB | 2       | 1205  | 0     | 3.30   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 2       | 2395  | 260   | 3.29   |
| Seagate   | ST3250318AS        | 250 GB | 14      | 1427  | 64    | 3.29   |
| Toshiba   | DT01ACA200         | 2 TB   | 14      | 1322  | 82    | 3.28   |
| HGST      | HUS726040ALN610    | 4 TB   | 3       | 1197  | 0     | 3.28   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 17      | 1196  | 0     | 3.28   |
| HGST      | HDN728080ALE604    | 8 TB   | 7       | 1182  | 0     | 3.24   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 4       | 1181  | 0     | 3.24   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 6       | 1178  | 0     | 3.23   |
| Hitachi   | HDS721050CLA660    | 500 GB | 7       | 1725  | 290   | 3.20   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 7       | 1514  | 13    | 3.20   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 3       | 1167  | 0     | 3.20   |
| WDC       | WD5000AACS-00ZUB0  | 500 GB | 2       | 1155  | 0     | 3.16   |
| Toshiba   | MG04ACA200E        | 2 TB   | 2       | 1149  | 0     | 3.15   |
| Fujitsu   | MHW2160BH PL       | 160 GB | 2       | 1148  | 0     | 3.15   |
| Hitachi   | HTS543216L9A300    | 160 GB | 2       | 1966  | 261   | 3.14   |
| WDC       | WD3000BLFS-60YBU2  | 304 GB | 2       | 1399  | 1     | 3.13   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 6       | 2271  | 46    | 3.13   |
| Seagate   | ST3500320AS        | 500 GB | 4       | 1671  | 98    | 3.10   |
| Samsung   | HD154UI            | 1.5 TB | 10      | 2394  | 221   | 3.10   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 9       | 1737  | 29    | 3.09   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 2       | 1128  | 0     | 3.09   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 2       | 1415  | 4     | 3.09   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 4       | 1116  | 0     | 3.06   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 2       | 2202  | 3     | 3.05   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 3       | 1110  | 0     | 3.04   |
| WDC       | WD3200BEKT-00KA9T0 | 320 GB | 2       | 1109  | 0     | 3.04   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 9       | 1704  | 3     | 3.04   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 13      | 1102  | 0     | 3.02   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 4       | 1803  | 2     | 3.01   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 8       | 1091  | 0     | 2.99   |
| WDC       | WD4002FYYZ-01B7CB0 | 4 TB   | 3       | 1087  | 0     | 2.98   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 3       | 1308  | 1     | 2.95   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 4       | 1254  | 10    | 2.95   |
| Samsung   | HD251HJ            | 250 GB | 2       | 1071  | 0     | 2.94   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 4       | 1919  | 326   | 2.91   |
| HGST      | HUS724040ALA640    | 4 TB   | 5       | 1058  | 0     | 2.90   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 40      | 1239  | 152   | 2.86   |
| Toshiba   | MQ01ABD100H        | 1 TB   | 2       | 1041  | 0     | 2.85   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 4       | 1250  | 1     | 2.85   |
| WDC       | WD5000LUCT-63RC2Y0 | 500 GB | 2       | 1038  | 0     | 2.84   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 11      | 1348  | 2     | 2.84   |
| Toshiba   | MC04ACA400E        | 4 TB   | 2       | 1023  | 0     | 2.80   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 11      | 1090  | 184   | 2.80   |
| Samsung   | HD322HJ            | 320 GB | 15      | 1299  | 80    | 2.80   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 10      | 1582  | 3     | 2.80   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 6       | 2362  | 8     | 2.79   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 12      | 1018  | 0     | 2.79   |
| ExcelStor | J8160              | 164 GB | 2       | 1015  | 0     | 2.78   |
| Samsung   | HD103UJ            | 1 TB   | 11      | 1726  | 23    | 2.78   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 3       | 2087  | 341   | 2.77   |
| WDC       | WD1600AAJS-60Z0A0  | 160 GB | 2       | 1445  | 803   | 2.77   |
| HPE       | MB4000GVYZK        | 4 TB   | 8       | 1005  | 0     | 2.76   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 4       | 1269  | 1     | 2.75   |
| Toshiba   | HDWE150            | 5 TB   | 6       | 1186  | 5     | 2.73   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 5       | 2630  | 386   | 2.73   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 8       | 1076  | 1     | 2.71   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 6       | 987   | 0     | 2.71   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 2       | 986   | 0     | 2.70   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 14      | 985   | 0     | 2.70   |
| Seagate   | ST91000640NS       | 1 TB   | 3       | 1405  | 1     | 2.70   |
| Seagate   | ST3160815AS        | 160 GB | 17      | 1699  | 244   | 2.69   |
| HGST      | HUS726T4TALA6L1    | 4 TB   | 4       | 981   | 0     | 2.69   |
| Seagate   | ST9160411AS        | 160 GB | 2       | 1221  | 3     | 2.68   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 4       | 1401  | 19    | 2.68   |
| Seagate   | ST3500413AS        | 500 GB | 23      | 1311  | 220   | 2.68   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 9       | 975   | 0     | 2.67   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 3       | 974   | 0     | 2.67   |
| Seagate   | ST3250312AS        | 250 GB | 14      | 1165  | 3     | 2.67   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 2       | 972   | 0     | 2.66   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 8       | 1235  | 3     | 2.66   |
| Samsung   | HD502HJ            | 500 GB | 10      | 1476  | 1     | 2.65   |
| WDC       | WD5000AAKS-75A7B0  | 500 GB | 2       | 968   | 0     | 2.65   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 1449  | 1     | 2.65   |
| Seagate   | ST3160318AS        | 160 GB | 16      | 1328  | 125   | 2.65   |
| Samsung   | HD501LJ            | 500 GB | 12      | 2110  | 256   | 2.64   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 22      | 1027  | 1     | 2.63   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 8       | 1069  | 2     | 2.61   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 2       | 950   | 0     | 2.60   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 4       | 950   | 0     | 2.60   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 19      | 945   | 0     | 2.59   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 4       | 1234  | 2     | 2.57   |
| WDC       | WD1001FALS-403AA0  | 1 TB   | 5       | 1345  | 166   | 2.57   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 8       | 1149  | 3     | 2.56   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 4       | 1240  | 93    | 2.54   |
| Seagate   | ST3320620NS        | 320 GB | 2       | 1617  | 1     | 2.54   |
| WDC       | WD1600AAJS-75M0A0  | 160 GB | 4       | 2270  | 14    | 2.53   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 10      | 1459  | 233   | 2.53   |
| HGST      | HDN721010ALE604    | 10 TB  | 3       | 916   | 0     | 2.51   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 2       | 1648  | 4     | 2.51   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 15      | 1035  | 1     | 2.51   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 14      | 1237  | 86    | 2.50   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 6       | 912   | 0     | 2.50   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 13      | 1144  | 2     | 2.49   |
| Seagate   | ST1000NM0018-2F... | 1 TB   | 2       | 910   | 0     | 2.49   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 3       | 907   | 0     | 2.49   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 2       | 906   | 0     | 2.48   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 6       | 1575  | 3     | 2.48   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1316  | 6     | 2.47   |
| Seagate   | ST9320421AS        | 320 GB | 2       | 1773  | 508   | 2.47   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 13      | 1796  | 585   | 2.47   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 5       | 1094  | 2     | 2.47   |
| Seagate   | ST3500312CS        | 500 GB | 17      | 1007  | 57    | 2.45   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 3       | 892   | 0     | 2.45   |
| Toshiba   | MD04ACA400         | 4 TB   | 4       | 920   | 3     | 2.43   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 3       | 1105  | 400   | 2.42   |
| Seagate   | ST32000542AS       | 2 TB   | 4       | 1296  | 241   | 2.41   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 12      | 878   | 0     | 2.41   |
| Hitachi   | HDP725025GLA380    | 250 GB | 2       | 1171  | 2     | 2.40   |
| Samsung   | HD753LJ            | 752 GB | 4       | 1723  | 423   | 2.40   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 22      | 973   | 53    | 2.38   |
| Seagate   | ST2000NE0025-2F... | 2 TB   | 3       | 868   | 0     | 2.38   |
| Seagate   | ST1000NM0011       | 1 TB   | 4       | 1690  | 8     | 2.37   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 8       | 863   | 0     | 2.37   |
| WDC       | WD40EFAX-68JH4N1   | 4 TB   | 4       | 861   | 0     | 2.36   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 6       | 1131  | 163   | 2.35   |
| Maxtor    | STM3250310AS       | 250 GB | 4       | 930   | 1     | 2.35   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 2       | 1242  | 3     | 2.33   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 6       | 2198  | 3     | 2.32   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 4       | 1160  | 2     | 2.32   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 2       | 928   | 1     | 2.32   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 9       | 1292  | 9     | 2.32   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 19      | 1259  | 29    | 2.32   |
| Hitachi   | HDS721050CLA662    | 500 GB | 2       | 844   | 0     | 2.32   |
| Samsung   | HM500JI            | 500 GB | 5       | 1054  | 42    | 2.31   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 4       | 904   | 1     | 2.30   |
| Seagate   | ST14000NM0018-2... | 14 TB  | 2       | 840   | 0     | 2.30   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 2       | 837   | 0     | 2.29   |
| WDC       | WD1600AAJS-40H3A0  | 160 GB | 3       | 834   | 0     | 2.29   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 10      | 918   | 1     | 2.27   |
| Maxtor    | STM3160815AS       | 160 GB | 3       | 1028  | 320   | 2.27   |
| HGST      | HUS726020ALA610    | 2 TB   | 2       | 822   | 0     | 2.25   |
| WDC       | WD1200BB-00HTA0    | 120 GB | 2       | 1633  | 347   | 2.24   |
| HGST      | HTS725050A7E635... | 500 GB | 2       | 1092  | 38    | 2.24   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 15      | 1289  | 149   | 2.23   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 2       | 810   | 0     | 2.22   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 2       | 810   | 0     | 2.22   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 4       | 1011  | 2     | 2.21   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 14      | 1690  | 578   | 2.21   |
| Fujitsu   | MHY2120BH          | 120 GB | 3       | 807   | 0     | 2.21   |
| WDC       | WD1600JS-00NCB1    | 160 GB | 2       | 807   | 0     | 2.21   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 8       | 807   | 0     | 2.21   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 3       | 1323  | 33    | 2.21   |
| Lenovo    | WD2004FBYZ-23YC... | 2 TB   | 4       | 802   | 0     | 2.20   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 2       | 802   | 0     | 2.20   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 30      | 890   | 3     | 2.20   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 4       | 1370  | 4     | 2.19   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 6       | 990   | 1     | 2.19   |
| Toshiba   | MG03ACA100         | 1 TB   | 11      | 800   | 0     | 2.19   |
| Seagate   | ST3000DM003-2AE16L | 3 TB   | 2       | 799   | 0     | 2.19   |
| Toshiba   | MG07ACA12TE        | 12 TB  | 5       | 797   | 0     | 2.19   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 2       | 833   | 4     | 2.18   |
| Apple     | HDD HTS541010A9... | 1 TB   | 7       | 907   | 1     | 2.17   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 30      | 1004  | 46    | 2.17   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 2       | 790   | 0     | 2.17   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 4       | 1097  | 2     | 2.16   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 10      | 817   | 54    | 2.16   |
| WDC       | WD2500AAKX-60U6AA0 | 250 GB | 2       | 781   | 0     | 2.14   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 12      | 1238  | 345   | 2.14   |
| WDC       | WD2500AAJS-00L7A0  | 250 GB | 2       | 1427  | 4     | 2.13   |
| WDC       | WD3200LPVX-08V0TT5 | 320 GB | 2       | 770   | 0     | 2.11   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 4       | 866   | 2     | 2.10   |
| Seagate   | ST3320418AS        | 320 GB | 9       | 1118  | 238   | 2.10   |
| Samsung   | HD080HJ            | 80 GB  | 2       | 760   | 0     | 2.08   |
| Seagate   | ST380817AS         | 80 GB  | 4       | 760   | 0     | 2.08   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 14      | 1041  | 128   | 2.08   |
| Samsung   | HD161GJ            | 160 GB | 5       | 934   | 429   | 2.08   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 6       | 756   | 0     | 2.07   |
| Seagate   | ST3320613AS        | 320 GB | 3       | 1341  | 11    | 2.07   |
| Seagate   | ST9160310AS        | 160 GB | 3       | 1465  | 2     | 2.07   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 2       | 754   | 0     | 2.07   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 6       | 1120  | 7     | 2.07   |
| WDC       | WD5000AAKX-00U6AA0 | 500 GB | 3       | 816   | 1     | 2.06   |
| Samsung   | HD203WI            | 2 TB   | 2       | 2609  | 4     | 2.04   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 44      | 781   | 5     | 2.03   |
| WDC       | WD10JMVW-11AJGS2   | 1 TB   | 2       | 754   | 52    | 2.02   |
| WDC       | WD1600BEVT-75ZCT2  | 160 GB | 5       | 735   | 0     | 2.01   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 12      | 734   | 0     | 2.01   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 3       | 728   | 0     | 2.00   |
| Toshiba   | DT01ACA100         | 1 TB   | 51      | 856   | 41    | 1.99   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 4       | 726   | 0     | 1.99   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 2       | 1577  | 4     | 1.97   |
| Seagate   | ST500DM002-1SB10A  | 500 GB | 8       | 718   | 0     | 1.97   |
| Hitachi   | HTS541060G9AT00    | 64 GB  | 2       | 973   | 3     | 1.97   |
| Toshiba   | MD04ACA500         | 5 TB   | 2       | 1203  | 23    | 1.97   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 12      | 783   | 1     | 1.96   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 15      | 796   | 1     | 1.96   |
| HGST      | HUS722T1TALA600    | 1 TB   | 2       | 713   | 0     | 1.95   |
| Toshiba   | HDWD120            | 2 TB   | 9       | 715   | 2     | 1.95   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 5       | 709   | 0     | 1.94   |
| Seagate   | ST3750528AS        | 752 GB | 5       | 1425  | 141   | 1.93   |
| Toshiba   | MK2561GSYN         | 250 GB | 2       | 702   | 0     | 1.92   |
| Toshiba   | HDWN180            | 8 TB   | 12      | 699   | 0     | 1.92   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 2       | 1368  | 4     | 1.91   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 3       | 696   | 0     | 1.91   |
| Toshiba   | DT01ACA050         | 500 GB | 36      | 887   | 52    | 1.90   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 91      | 715   | 1     | 1.89   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 3       | 1050  | 336   | 1.88   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 10      | 806   | 2     | 1.87   |
| WDC       | WD2500BEKT-75PVMT0 | 250 GB | 2       | 921   | 3     | 1.87   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 16      | 677   | 0     | 1.86   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 104     | 1099  | 162   | 1.85   |
| Seagate   | ST3000NM0005-1V... | 3 TB   | 4       | 669   | 0     | 1.84   |
| Hitachi   | HTS725032A9A364    | 320 GB | 5       | 1055  | 205   | 1.83   |
| Seagate   | ST10000DM0004-1... | 10 TB  | 2       | 664   | 0     | 1.82   |
| Hitachi   | HDS721032CLA362    | 320 GB | 2       | 848   | 1030  | 1.81   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 4       | 659   | 0     | 1.81   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 3       | 1707  | 398   | 1.81   |
| Seagate   | ST3320620AS        | 320 GB | 11      | 1175  | 333   | 1.81   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 4       | 655   | 0     | 1.80   |
| Seagate   | ST380013AS         | 80 GB  | 6       | 1319  | 5     | 1.79   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 2       | 649   | 0     | 1.78   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 3       | 885   | 1     | 1.77   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 12      | 672   | 3     | 1.76   |
| WDC       | WD10SPZX-75Z10T2   | 1 TB   | 3       | 632   | 0     | 1.73   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 14      | 683   | 2     | 1.73   |
| Seagate   | ST3160813AS        | 160 GB | 4       | 839   | 1     | 1.72   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 2       | 623   | 0     | 1.71   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 3       | 622   | 0     | 1.71   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 5       | 620   | 0     | 1.70   |
| WDC       | WD3200AAKS-75L9A0  | 320 GB | 4       | 1552  | 5     | 1.70   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 2       | 616   | 0     | 1.69   |
| HGST      | HUS726040ALE610    | 4 TB   | 3       | 1030  | 464   | 1.68   |
| Seagate   | ST3160023AS        | 160 GB | 2       | 1239  | 3     | 1.68   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 8       | 601   | 0     | 1.65   |
| WDC       | WD2500BEVT-22ZCT0  | 250 GB | 3       | 716   | 1     | 1.64   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 4       | 796   | 416   | 1.64   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 35      | 607   | 1     | 1.63   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 8       | 699   | 1     | 1.63   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 2       | 593   | 0     | 1.63   |
| WDC       | WD2500YS-01SHB1    | 256 GB | 2       | 589   | 0     | 1.61   |
| Fujitsu   | MHW2120BH          | 120 GB | 4       | 658   | 5     | 1.61   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 6       | 643   | 2     | 1.61   |
| Hitachi   | HTS727550A9E364    | 500 GB | 7       | 909   | 313   | 1.61   |
| WDC       | WD5000AAKX-083CA0  | 500 GB | 2       | 2132  | 5     | 1.60   |
| Samsung   | HD250HJ            | 250 GB | 2       | 1067  | 1211  | 1.59   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 6       | 580   | 0     | 1.59   |
| Toshiba   | HDWQ140            | 4 TB   | 22      | 579   | 0     | 1.59   |
| Samsung   | SP2504C            | 250 GB | 2       | 716   | 506   | 1.59   |
| Hitachi   | HCS5C1032CLA382    | 320 GB | 2       | 1409  | 3     | 1.58   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 2       | 575   | 0     | 1.58   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 5       | 838   | 3     | 1.57   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 3       | 573   | 0     | 1.57   |
| Seagate   | ST31000524AS       | 1 TB   | 12      | 977   | 199   | 1.57   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 3       | 1376  | 3     | 1.57   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 2       | 789   | 1     | 1.54   |
| Hitachi   | HTS545032B9A300    | 320 GB | 14      | 617   | 172   | 1.53   |
| Hitachi   | HDS721050CLA362    | 500 GB | 4       | 615   | 254   | 1.53   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 4       | 556   | 0     | 1.53   |
| Seagate   | ST9250410AS        | 250 GB | 12      | 614   | 33    | 1.51   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 9       | 597   | 42    | 1.49   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 14      | 654   | 1     | 1.49   |
| Seagate   | ST10000DM0004-2... | 10 TB  | 4       | 1074  | 358   | 1.48   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 18      | 597   | 1     | 1.48   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 2       | 537   | 0     | 1.47   |
| HPE       | MB0500GCEHE        | 500 GB | 8       | 633   | 35    | 1.47   |
| Toshiba   | HDWD130            | 3 TB   | 15      | 719   | 4     | 1.47   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 30      | 722   | 9     | 1.44   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 17      | 778   | 336   | 1.44   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 3       | 554   | 1     | 1.43   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 18      | 623   | 55    | 1.42   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 4       | 517   | 0     | 1.42   |
| Toshiba   | MQ01ACF050         | 500 GB | 15      | 539   | 1     | 1.41   |
| WDC       | WD20EZRZ-22Z5HB0   | 2 TB   | 3       | 514   | 0     | 1.41   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 3       | 513   | 0     | 1.41   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 15      | 987   | 11    | 1.40   |
| WDC       | WD3200BPVT-22ZEST0 | 320 GB | 2       | 509   | 0     | 1.40   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 14      | 517   | 2     | 1.39   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 8       | 1309  | 7     | 1.38   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 6       | 989   | 173   | 1.38   |
| Seagate   | ST3750640AS        | 752 GB | 2       | 1505  | 2     | 1.38   |
| Seagate   | ST3500418AS        | 500 GB | 36      | 1144  | 100   | 1.36   |
| Hitachi   | HTS545016B9A300    | 160 GB | 5       | 653   | 4     | 1.36   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 33      | 494   | 0     | 1.36   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 15      | 569   | 72    | 1.35   |
| HGST      | HTE545032A7E380    | 320 GB | 4       | 628   | 4     | 1.34   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 2       | 486   | 0     | 1.33   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 10      | 486   | 0     | 1.33   |
| Seagate   | ST500NM0011        | 500 GB | 4       | 1849  | 20    | 1.31   |
| Samsung   | HM250HI            | 250 GB | 8       | 554   | 12    | 1.30   |
| Hitachi   | HTS545025B9A300    | 250 GB | 13      | 512   | 156   | 1.30   |
| Toshiba   | MQ01ABD100V        | 1 TB   | 2       | 474   | 0     | 1.30   |
| Seagate   | ST6000NE0023-2E... | 6 TB   | 2       | 853   | 4     | 1.30   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 9       | 557   | 8     | 1.30   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 11      | 530   | 1     | 1.29   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 6       | 471   | 0     | 1.29   |
| WDC       | WD3200BPVT-55ZEST0 | 320 GB | 2       | 496   | 1     | 1.26   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 14      | 512   | 2     | 1.26   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 2       | 457   | 0     | 1.25   |
| WDC       | WD80EDAZ-11TA3A0   | 8 TB   | 3       | 621   | 1     | 1.25   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 10      | 455   | 0     | 1.25   |
| Seagate   | ST500LM000-1EJ162  | 500 GB | 14      | 621   | 6     | 1.25   |
| HGST      | HTS721010A9E630    | 1 TB   | 38      | 594   | 223   | 1.24   |
| Samsung   | HD103SI            | 1 TB   | 8       | 941   | 483   | 1.24   |
| Toshiba   | MQ01ACF032         | 320 GB | 9       | 573   | 176   | 1.23   |
| Seagate   | ST4000LM024-2U817V | 4 TB   | 4       | 447   | 0     | 1.23   |
| WDC       | WD40EZAZ-22SF3B0   | 4 TB   | 4       | 446   | 0     | 1.22   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 9       | 444   | 0     | 1.22   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 2       | 856   | 68    | 1.22   |
| Hitachi   | HDT725032VLA380    | 320 GB | 2       | 441   | 0     | 1.21   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 12      | 440   | 0     | 1.21   |
| Seagate   | ST4000DM004-2U9104 | 4 TB   | 3       | 439   | 0     | 1.20   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 4       | 438   | 0     | 1.20   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 4       | 438   | 0     | 1.20   |
| Seagate   | ST3320820AS        | 320 GB | 3       | 437   | 0     | 1.20   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 3       | 578   | 6     | 1.20   |
| Samsung   | HD161HJ            | 160 GB | 8       | 692   | 330   | 1.20   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 2       | 695   | 1     | 1.19   |
| Hitachi   | HTS541080G9SA00    | 80 GB  | 2       | 565   | 1     | 1.19   |
| Samsung   | HD160JJ            | 160 GB | 2       | 1414  | 3     | 1.19   |
| HGST      | HUS726060ALE614    | 6 TB   | 4       | 430   | 0     | 1.18   |
| WDC       | WD80EFZZ-68BTXN0   | 8 TB   | 2       | 429   | 0     | 1.18   |
| Seagate   | ST96812AS          | 64 GB  | 7       | 496   | 6     | 1.17   |
| WDC       | WD2000FYYZ         | 2 TB   | 2       | 1353  | 3     | 1.17   |
| WDC       | WD80EFBX-68AZZN0   | 8 TB   | 2       | 425   | 0     | 1.17   |
| Samsung   | HM321HI            | 320 GB | 9       | 557   | 118   | 1.16   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 58      | 460   | 10    | 1.16   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 2       | 424   | 0     | 1.16   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 55      | 600   | 3     | 1.15   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 33      | 418   | 0     | 1.15   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 14      | 414   | 0     | 1.13   |
| Fujitsu   | MHY2200BH          | 200 GB | 2       | 412   | 0     | 1.13   |
| HGST      | HUS722T2TALA604    | 2 TB   | 6       | 505   | 3     | 1.13   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 4       | 663   | 259   | 1.12   |
| HGST      | HTS725032A7E630    | 320 GB | 10      | 723   | 15    | 1.12   |
| Seagate   | ST3160215AS        | 160 GB | 3       | 592   | 784   | 1.12   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 12      | 998   | 55    | 1.12   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 7       | 408   | 0     | 1.12   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 4       | 406   | 0     | 1.11   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 9       | 403   | 0     | 1.11   |
| WDC       | WD20SDRW-11VUUS1   | 2 TB   | 2       | 403   | 0     | 1.11   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 57      | 432   | 5     | 1.10   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 3       | 805   | 1     | 1.10   |

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
| HP          | 6      | 28      | 2308  | 2     | 4.69   |
| Hitachi     | 81     | 430     | 1397  | 141   | 2.83   |
| WDC         | 355    | 1930    | 1111  | 28    | 2.44   |
| HGST        | 41     | 356     | 997   | 164   | 2.32   |
| Samsung     | 38     | 208     | 1387  | 184   | 2.32   |
| HPE         | 5      | 35      | 1058  | 182   | 2.25   |
| Lenovo      | 1      | 4       | 802   | 0     | 2.20   |
| Maxtor      | 7      | 19      | 829   | 177   | 1.86   |
| Seagate     | 219    | 2003    | 842   | 134   | 1.68   |
| ExcelStor   | 2      | 4       | 1009  | 8     | 1.64   |
| Fujitsu     | 8      | 19      | 608   | 67    | 1.46   |
| Toshiba     | 88     | 607     | 625   | 64    | 1.36   |
| Apple       | 4      | 25      | 536   | 99    | 1.33   |
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
| Samsung   | MZ7LM1T9HCJM-00003 | 1.9 TB | 2       | 2953  | 0     | 8.09   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 2       | 2891  | 0     | 7.92   |
| HPE       | MK0100GCTYU        | 100 GB | 2       | 2727  | 0     | 7.47   |
| HPE       | MK0400GCTZA        | 400 GB | 2       | 2705  | 0     | 7.41   |
| Intel     | SSDSC2BB240G6      | 240 GB | 3       | 2692  | 0     | 7.38   |
| Corsair   | Force 3 SSD        | 240 GB | 2       | 2608  | 0     | 7.15   |
| PNY       | CS2211 240GB SSD   | 240 GB | 2       | 2519  | 0     | 6.90   |
| Intel     | SSDMCEAC120B3      | 120 GB | 2       | 2427  | 0     | 6.65   |
| Intel     | SSDSC2BA100G3L     | 100 GB | 4       | 2369  | 0     | 6.49   |
| Intel     | SSDSC2BB160G4      | 160 GB | 4       | 2330  | 0     | 6.38   |
| OCZ       | AGILITY            | 32 GB  | 2       | 2269  | 0     | 6.22   |
| Intel     | SSDSC2BA800G3      | 800 GB | 2       | 2898  | 1     | 6.15   |
| HP        | VK0800GDJYA        | 800 GB | 2       | 2239  | 0     | 6.14   |
| OCZ       | VERTEX2            | 64 GB  | 2       | 2221  | 0     | 6.09   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 2       | 2205  | 0     | 6.04   |
| ADATA     | SP310              | 64 GB  | 3       | 2184  | 0     | 5.98   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 6       | 2406  | 1     | 5.86   |
| ADATA     | SP310              | 128 GB | 2       | 2109  | 0     | 5.78   |
| Apple     | SSD SM0256F        | 256 GB | 2       | 2089  | 0     | 5.72   |
| Samsung   | MZ7PC128HAFU-000H1 | 128 GB | 2       | 2013  | 0     | 5.52   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 2       | 2007  | 0     | 5.50   |
| Intel     | SSDSC2BB120G7K     | 120 GB | 2       | 1961  | 0     | 5.37   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 7       | 1928  | 0     | 5.28   |
| ADATA     | SP310              | 32 GB  | 2       | 1914  | 0     | 5.25   |
| HP        | VK0300GDUQV        | 304 GB | 2       | 2751  | 1     | 5.02   |
| Apple     | SSD SM512E         | 500 GB | 3       | 1811  | 0     | 4.96   |
| Intel     | TK0080GDSAE        | 80 GB  | 2       | 1800  | 0     | 4.93   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 24      | 1795  | 0     | 4.92   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 2       | 1793  | 0     | 4.91   |
| Intel     | SSDSC2BA200G4      | 200 GB | 3       | 1759  | 0     | 4.82   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 2       | 1756  | 0     | 4.81   |
| Seagate   | XF1230-1A0240      | 240 GB | 2       | 1752  | 0     | 4.80   |
| SanDisk   | SDSSDH120GG25      | 120 GB | 2       | 1744  | 0     | 4.78   |
| Intel     | SSDSC2BP240G4      | 240 GB | 4       | 1710  | 0     | 4.69   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 18      | 1707  | 0     | 4.68   |
| Samsung   | SSD 830 Series     | 256 GB | 7       | 1672  | 0     | 4.58   |
| OCZ       | VERTEX4            | 256 GB | 3       | 1660  | 0     | 4.55   |
| Corsair   | Force GS           | 128 GB | 3       | 1654  | 0     | 4.53   |
| WDC       | WDS400T1R0A-68A4W0 | 4 TB   | 2       | 1650  | 0     | 4.52   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 4       | 1619  | 0     | 4.44   |
| Samsung   | SSD 850 PRO        | 128 GB | 22      | 1618  | 0     | 4.44   |
| Goodram   | SSD                | 64 GB  | 2       | 1615  | 0     | 4.43   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 21      | 1889  | 102   | 4.38   |
| Intel     | SSDSC2KB960G7      | 960 GB | 2       | 1595  | 0     | 4.37   |
| Samsung   | MZ7PD256HCGM-000H7 | 256 GB | 6       | 1579  | 0     | 4.33   |
| Corsair   | Force 3 SSD        | 64 GB  | 5       | 1572  | 0     | 4.31   |
| HP        | VK000480GWCNQ      | 480 GB | 2       | 1572  | 0     | 4.31   |
| Intel     | SSDSC2BA100G3      | 100 GB | 3       | 1558  | 0     | 4.27   |
| SanDisk   | SDSSDXP480G        | 480 GB | 2       | 1552  | 0     | 4.25   |
| WDC       | WDS250G2B0B        | 250 GB | 2       | 1526  | 0     | 4.18   |
| Intel     | SSDSC2BB240G7      | 240 GB | 2       | 1512  | 0     | 4.14   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 20      | 1547  | 102   | 4.13   |
| HP        | VK000240GWEZB      | 240 GB | 3       | 1502  | 0     | 4.12   |
| Samsung   | SSD 840 EVO        | 120 GB | 48      | 1692  | 11    | 4.10   |
| Intel     | SSDSC2BB800G4      | 800 GB | 2       | 1490  | 0     | 4.08   |
| OCZ       | VERTEX2            | 120 GB | 3       | 1489  | 0     | 4.08   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 3       | 1483  | 0     | 4.06   |
| Samsung   | MZ-5EA2000-0D3     | 200 GB | 4       | 1481  | 0     | 4.06   |
| Samsung   | SSD 840 EVO        | 500 GB | 8       | 1549  | 105   | 4.05   |
| OCZ       | VERTEX3            | 64 GB  | 7       | 1852  | 5     | 4.05   |
| Micron    | M600_MTFDDAK128MBF | 128 GB | 3       | 1475  | 0     | 4.04   |
| Kingston  | SUV300S37A120G     | 120 GB | 2       | 1473  | 0     | 4.04   |
| Intel     | SSDSC2BB080G6      | 80 GB  | 2       | 1466  | 0     | 4.02   |
| Toshiba   | THNSNJ128GCSY      | 128 GB | 2       | 1463  | 0     | 4.01   |
| SanDisk   | SDSA6DM-016G-1006  | 16 GB  | 2       | 1457  | 0     | 3.99   |
| OCZ       | VERTEX3 MI         | 120 GB | 2       | 2104  | 1     | 3.97   |
| SanDisk   | SDSA6PM-064G-1006  | 64 GB  | 4       | 1444  | 0     | 3.96   |
| HP        | VK0240GEFJF        | 240 GB | 2       | 1441  | 0     | 3.95   |
| Micron    | 5100_MTFDDAK480TCB | 480 GB | 2       | 1440  | 0     | 3.95   |
| Intel     | SSDSC2CT180A3      | 180 GB | 4       | 1901  | 1     | 3.88   |
| Intel     | SSDMCEAC030B3      | 32 GB  | 10      | 1415  | 0     | 3.88   |
| Kingston  | SVP200S3120G       | 120 GB | 2       | 1411  | 0     | 3.87   |
| Intel     | SSDSA2CW160G3      | 160 GB | 6       | 1384  | 0     | 3.79   |
| Intel     | SSDSA2CW120G3      | 120 GB | 10      | 1382  | 0     | 3.79   |
| SanDisk   | SDSSDHP128G        | 128 GB | 3       | 1377  | 0     | 3.77   |
| HP        | FK0032CAAZP        | 32 GB  | 3       | 1371  | 0     | 3.76   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 3       | 1934  | 3     | 3.72   |
| SanDisk   | SSD U100           | 8 GB   | 2       | 1358  | 0     | 3.72   |
| Seagate   | ST240HM000-1G5152  | 240 GB | 2       | 1356  | 0     | 3.72   |
| Samsung   | MZMTE128HMGR-00007 | 128 GB | 3       | 1452  | 1     | 3.72   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 6       | 1439  | 1     | 3.71   |
| Samsung   | SSD 830 Series     | 128 GB | 19      | 1488  | 54    | 3.71   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 3       | 1494  | 1     | 3.68   |
| ADATA     | SP900              | 64 GB  | 3       | 1342  | 0     | 3.68   |
| Kingmax   | SSD                | 240 GB | 2       | 1341  | 0     | 3.68   |
| Micron    | M600_MTFDDAT128MBF | 128 GB | 3       | 1340  | 0     | 3.67   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 4       | 1337  | 0     | 3.67   |
| SanDisk   | SDMSATA512G        | 512 GB | 2       | 1323  | 0     | 3.63   |
| Samsung   | SSD 840 PRO Series | 512 GB | 8       | 1316  | 0     | 3.61   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 3       | 1550  | 341   | 3.57   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 2       | 1303  | 0     | 3.57   |
| Kingston  | SVP200S37A60G      | 64 GB  | 5       | 1297  | 0     | 3.56   |
| Samsung   | MZ7LM240HCGR-0E003 | 240 GB | 2       | 1295  | 0     | 3.55   |
| Samsung   | SSD 830 Series     | 64 GB  | 6       | 1294  | 0     | 3.55   |
| SanDisk   | SDSSDH2128G        | 128 GB | 2       | 1293  | 0     | 3.55   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 3       | 1279  | 0     | 3.51   |
| HPE       | MK000480GWCEV      | 480 GB | 2       | 1275  | 0     | 3.49   |
| HPE       | MK000960GWCFA      | 960 GB | 2       | 1275  | 0     | 3.49   |
| PNY       | CS1311 240GB SSD   | 240 GB | 6       | 1271  | 0     | 3.48   |
| Seagate   | XF1230-1A0480      | 480 GB | 2       | 1266  | 0     | 3.47   |
| Intel     | SSDSC2BA400G3      | 400 GB | 3       | 1496  | 1     | 3.39   |
| Toshiba   | THNSNH128GBST      | 128 GB | 3       | 1235  | 0     | 3.38   |
| Samsung   | SSD 840 Series     | 250 GB | 15      | 1230  | 0     | 3.37   |
| Samsung   | SSD CM871 2.5 7mm  | 128 GB | 2       | 1228  | 0     | 3.37   |
| Intel     | SSDSC2CT240A3      | 240 GB | 2       | 2264  | 4     | 3.36   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 7       | 1225  | 0     | 3.36   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 2       | 1224  | 0     | 3.35   |
| Toshiba   | Q300 Pro           | 128 GB | 3       | 1215  | 0     | 3.33   |
| Apacer    | 4GB SATA Flash ... | 4 GB   | 2       | 1210  | 0     | 3.32   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 4       | 1490  | 522   | 3.31   |
| SanDisk   | SDSSDX120GG25      | 120 GB | 3       | 1193  | 0     | 3.27   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 4       | 1188  | 0     | 3.26   |
| SanDisk   | SSD U100           | 24 GB  | 5       | 1184  | 0     | 3.25   |
| OCZ       | AGILITY3           | 120 GB | 15      | 1459  | 127   | 3.24   |
| Intel     | SSDSC2BB150G7      | 150 GB | 12      | 1346  | 1     | 3.23   |
| Intel     | SSDSC2BB960G7R     | 960 GB | 6       | 1177  | 0     | 3.23   |
| Samsung   | SSD PB22-JS3 FD... | 128 GB | 2       | 1176  | 0     | 3.22   |
| Dell      | SSDSCKJB120G7R     | 120 GB | 2       | 1173  | 0     | 3.22   |
| Intel     | SSDSC2BB120G4      | 120 GB | 17      | 1238  | 1     | 3.20   |
| Apple     | SSD TS128C         | 121 GB | 4       | 1161  | 0     | 3.18   |
| ADATA     | SP600              | 128 GB | 4       | 1155  | 0     | 3.16   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 1154  | 0     | 3.16   |
| Samsung   | MZNLN256HCHP-000H1 | 256 GB | 4       | 1142  | 0     | 3.13   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 11      | 1279  | 162   | 3.12   |
| SanDisk   | Ultra II           | 960 GB | 3       | 1137  | 0     | 3.12   |
| Kingston  | SUV300S37A240G     | 240 GB | 2       | 1135  | 0     | 3.11   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 2       | 1125  | 0     | 3.08   |
| Intel     | SSDSC2CT180A4      | 180 GB | 4       | 1469  | 1     | 3.05   |
| Samsung   | SSD 840 PRO Series | 128 GB | 29      | 1215  | 68    | 3.05   |
| Patriot   | Flare              | 64 GB  | 2       | 1107  | 0     | 3.03   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 7       | 1104  | 0     | 3.03   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 2       | 1226  | 1     | 3.03   |
| Intel     | SSDSC2KB240G7      | 240 GB | 5       | 1102  | 0     | 3.02   |
| Intel     | SSDSC2BB300G4      | 304 GB | 2       | 1094  | 0     | 3.00   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 3       | 1090  | 0     | 2.99   |
| Samsung   | MZMPC128HBFU-000H1 | 128 GB | 4       | 1087  | 0     | 2.98   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 8       | 1081  | 0     | 2.96   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 3       | 1077  | 0     | 2.95   |
| WDC       | WDS500G1B0B-00AS40 | 500 GB | 2       | 1072  | 0     | 2.94   |
| Samsung   | SSD 840 Series     | 120 GB | 27      | 1195  | 41    | 2.92   |
| Samsung   | SSD 850 EVO        | 120 GB | 41      | 1062  | 0     | 2.91   |
| Kingston  | SKC400S37512G      | 512 GB | 2       | 1059  | 0     | 2.90   |
| Intel     | SSDSC2CW240A3      | 240 GB | 8       | 1054  | 0     | 2.89   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 3       | 1045  | 0     | 2.86   |
| Indilinx  | IND-S3MP-128G      | 128 GB | 2       | 1043  | 0     | 2.86   |
| Crucial   | CT240M500SSD3      | 240 GB | 3       | 1043  | 0     | 2.86   |
| Corsair   | Force GT           | 240 GB | 2       | 1042  | 0     | 2.86   |
| Samsung   | MZ7LN512HMJP-000L1 | 512 GB | 2       | 1041  | 0     | 2.85   |
| Samsung   | SSD 840 EVO        | 250 GB | 57      | 1097  | 8     | 2.85   |
| Intel     | SSDSC2BA400G4      | 400 GB | 3       | 1508  | 1     | 2.85   |
| Intel     | SSDSC2BB480G4      | 480 GB | 4       | 1920  | 253   | 2.83   |
| Kingston  | SH103S3120G        | 120 GB | 9       | 1172  | 3     | 2.83   |
| Samsung   | SSD 850 PRO        | 512 GB | 31      | 1031  | 0     | 2.83   |
| ADATA     | SP600              | 32 GB  | 4       | 1428  | 2     | 2.82   |
| Crucial   | CT250MX200SSD1     | 250 GB | 7       | 1063  | 1     | 2.77   |
| Lite-On   | LAT-256M3S         | 256 GB | 2       | 1011  | 0     | 2.77   |
| Samsung   | SSD 850 PRO        | 1 TB   | 10      | 1196  | 4     | 2.76   |
| Patriot   | Blaze              | 64 GB  | 2       | 1006  | 0     | 2.76   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 4       | 995   | 0     | 2.73   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 6       | 994   | 0     | 2.72   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 24      | 993   | 0     | 2.72   |
| Toshiba   | THNSFJ256GDNU      | 256 GB | 3       | 992   | 0     | 2.72   |
| Samsung   | SSD 750 EVO        | 250 GB | 15      | 984   | 0     | 2.70   |
| OCZ       | AGILITY3           | 64 GB  | 9       | 1093  | 1     | 2.69   |
| Crucial   | FCCT128M4SSD1      | 128 GB | 3       | 979   | 0     | 2.68   |
| Samsung   | SSD 860 EVO        | 2 TB   | 5       | 978   | 0     | 2.68   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 20      | 975   | 0     | 2.67   |
| GAMER     | L TA1D0120A        | 120 GB | 2       | 970   | 0     | 2.66   |
| Apple     | SSD SM128C         | 121 GB | 2       | 1150  | 317   | 2.66   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 3       | 969   | 0     | 2.66   |
| Micron    | MTFDDAV256TDL      | 256 GB | 2       | 965   | 0     | 2.64   |
| OCZ       | AGILITY3           | 240 GB | 3       | 1449  | 5     | 2.64   |
| Crucial   | CT256MX100SSD1     | 256 GB | 14      | 1021  | 1     | 2.64   |
| Samsung   | MZNLN512HMJP-000H1 | 512 GB | 2       | 955   | 0     | 2.62   |
| Transcend | TS64GMTS400S       | 64 GB  | 3       | 954   | 0     | 2.61   |
| OCZ       | VERTEX4            | 128 GB | 5       | 1130  | 1     | 2.61   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 6       | 945   | 0     | 2.59   |
| Patriot   | Pyro               | 64 GB  | 3       | 943   | 0     | 2.59   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 2       | 935   | 0     | 2.56   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 3       | 933   | 0     | 2.56   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 19      | 929   | 0     | 2.55   |
| ADATA     | IM2S3134N-064GM    | 64 GB  | 58      | 928   | 0     | 2.54   |
| Samsung   | SSD 840 PRO Series | 256 GB | 25      | 1279  | 50    | 2.54   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 9       | 914   | 0     | 2.50   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 2       | 911   | 0     | 2.50   |
| Samsung   | MZMTD128HAFV-000L1 | 128 GB | 2       | 911   | 0     | 2.50   |
| Samsung   | SSD 850 EVO        | 1 TB   | 24      | 1108  | 1     | 2.49   |
| SuperM... | SSD                | 64 GB  | 7       | 909   | 0     | 2.49   |
| ADATA     | SSD S510           | 64 GB  | 2       | 908   | 0     | 2.49   |
| SanDisk   | SSD U100           | 32 GB  | 5       | 905   | 0     | 2.48   |
| Samsung   | SSD PM871b 2.5 7mm | 512 GB | 2       | 901   | 0     | 2.47   |
| Samsung   | SSD 850 EVO        | 250 GB | 161     | 934   | 1     | 2.47   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 10      | 898   | 0     | 2.46   |
| Samsung   | SSD 750 EVO        | 120 GB | 15      | 896   | 0     | 2.46   |
| OCZ       | VERTEX460A         | 120 GB | 2       | 895   | 0     | 2.45   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 3       | 893   | 0     | 2.45   |
| Samsung   | SSD 850 PRO        | 256 GB | 43      | 921   | 1     | 2.45   |
| Crucial   | CT250MX200SSD3     | 250 GB | 2       | 892   | 0     | 2.45   |
| Innodisk  | DEMSR- 08GB mSA... | 8 GB   | 10      | 890   | 0     | 2.44   |
| Samsung   | SSD 850 EVO        | 500 GB | 84      | 916   | 1     | 2.44   |
| Goodram   | SSD                | 240 GB | 6       | 886   | 0     | 2.43   |
| HPE       | MK000240GWEZF      | 240 GB | 2       | 882   | 0     | 2.42   |
| Kingston  | SMS200S330G        | 32 GB  | 15      | 1207  | 2     | 2.40   |
| Kingston  | SNV425S264GB       | 64 GB  | 2       | 882   | 3     | 2.40   |
| Transcend | TS256GSSD370       | 256 GB | 2       | 872   | 0     | 2.39   |
| SK hynix  | SC311 SATA         | 512 GB | 7       | 861   | 0     | 2.36   |
| Kingston  | SUV500M8480G       | 480 GB | 2       | 860   | 0     | 2.36   |
| China     | SATA SSD           | 16 GB  | 107     | 879   | 1     | 2.36   |
| Samsung   | SSD 840 EVO 500... | 500 GB | 2       | 849   | 0     | 2.33   |
| Samsung   | MZMPC032HBCD-000L1 | 32 GB  | 3       | 847   | 0     | 2.32   |
| Kingston  | SHFS37A120G        | 120 GB | 20      | 1120  | 2     | 2.32   |
| WDC       | WDBNCE5000PNC      | 500 GB | 5       | 845   | 0     | 2.32   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 3       | 839   | 0     | 2.30   |
| Micron    | P300-MTFDDAC100SAL | 100 GB | 2       | 1551  | 503   | 2.30   |
| Samsung   | MZ7TE256HMHP-000L7 | 256 GB | 2       | 835   | 0     | 2.29   |
| Kingston  | SH103S3240G        | 240 GB | 6       | 1129  | 302   | 2.29   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 6       | 835   | 0     | 2.29   |
| Intel     | SSDSCKHB120G4      | 120 GB | 2       | 834   | 0     | 2.29   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 7       | 888   | 1     | 2.29   |
| Indilinx  | IND-S3MP-64G       | 64 GB  | 2       | 826   | 0     | 2.27   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 6       | 823   | 0     | 2.26   |
| Intel     | SSDSC2BB480G7      | 480 GB | 3       | 940   | 1     | 2.26   |
| Pioneer   | APS-SL3N-256       | 256 GB | 2       | 822   | 0     | 2.25   |
| SanDisk   | SDSSDHII240G       | 240 GB | 4       | 819   | 0     | 2.25   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 3       | 818   | 0     | 2.24   |
| ADATA     | SP920SS            | 128 GB | 2       | 816   | 0     | 2.24   |
| OCZ       | VERTEX3            | 120 GB | 10      | 1294  | 19    | 2.23   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 7       | 808   | 0     | 2.22   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 3       | 805   | 0     | 2.21   |
| SanDisk   | SSD i100           | 32 GB  | 4       | 1463  | 4     | 2.19   |
| WDC       | WDS240G1G0B-00RC30 | 240 GB | 2       | 797   | 0     | 2.19   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 5       | 797   | 0     | 2.19   |
| SanDisk   | X300 MSATA         | 256 GB | 2       | 792   | 0     | 2.17   |
| Intel     | SSDSC2BB120G6      | 120 GB | 4       | 791   | 0     | 2.17   |
| Crucial   | CT960M500SSD1      | 960 GB | 2       | 787   | 0     | 2.16   |
| Crucial   | CT240M500SSD1      | 240 GB | 13      | 1218  | 210   | 2.15   |
| Kingston  | SNV425S2128GB      | 128 GB | 4       | 1585  | 4     | 2.15   |
| SanDisk   | SDSSDH3250G        | 250 GB | 2       | 783   | 0     | 2.15   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 2       | 782   | 0     | 2.14   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 5       | 778   | 0     | 2.13   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 12      | 778   | 0     | 2.13   |
| Intel     | SSDSC2BW120A4      | 120 GB | 24      | 775   | 0     | 2.13   |
| Mushkin   | MKNSSDRE512GB-XT   | 512 GB | 2       | 774   | 0     | 2.12   |
| Intel     | SSDSC2KG240G7      | 240 GB | 2       | 1289  | 2     | 2.12   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 2       | 1119  | 165   | 2.12   |
| Kingston  | SMS200S360G        | 64 GB  | 27      | 1287  | 89    | 2.11   |
| Kingston  | SV300S37A120G      | 120 GB | 88      | 934   | 3     | 2.11   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 2       | 770   | 0     | 2.11   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 8       | 764   | 0     | 2.10   |
| OCZ       | TRION150           | 240 GB | 5       | 763   | 0     | 2.09   |
| Toshiba   | Q300               | 480 GB | 2       | 762   | 0     | 2.09   |
| Samsung   | SSD 850 EVO        | 2 TB   | 2       | 759   | 0     | 2.08   |
| Samsung   | MZYLN256HCHP-000L2 | 256 GB | 2       | 758   | 0     | 2.08   |
| ADATA     | SP900              | 128 GB | 8       | 756   | 0     | 2.07   |
| Corsair   | Force LS SSD       | 64 GB  | 9       | 1001  | 113   | 2.07   |
| Intel     | SSDSC2KB960G8      | 960 GB | 5       | 754   | 0     | 2.07   |
| AMD       | R3SL120G           | 120 GB | 4       | 807   | 1     | 2.07   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 7       | 1189  | 9     | 2.05   |
| Intel     | SSDMCEAC060B3      | 64 GB  | 5       | 864   | 1     | 2.05   |
| Hoodisk   | SSD                | 32 GB  | 79      | 746   | 0     | 2.05   |
| SanDisk   | SDSSDH31000G       | 1 TB   | 2       | 744   | 0     | 2.04   |
| SanDisk   | SDSSDP064G         | 64 GB  | 16      | 770   | 9     | 2.04   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 2       | 743   | 0     | 2.04   |
| Phison    | SATA SSD           | 120 GB | 4       | 741   | 0     | 2.03   |
| Samsung   | SSD 840 EVO        | 1 TB   | 7       | 739   | 0     | 2.03   |
| Samsung   | SSD RBX Series ... | 64 GB  | 2       | 739   | 0     | 2.03   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 4       | 737   | 0     | 2.02   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 4       | 736   | 0     | 2.02   |
| Crucial   | CT120M500SSD3      | 120 GB | 3       | 1187  | 6     | 2.01   |
| SanDisk   | SD9SB8W-256G-1006  | 256 GB | 3       | 732   | 0     | 2.01   |
| Kingston  | SUV400S37240G      | 240 GB | 18      | 775   | 1     | 2.00   |
| Hoodisk   | SSD                | 16 GB  | 21      | 729   | 0     | 2.00   |
| Protectli | 16GB mSATA         | 16 GB  | 2       | 728   | 0     | 2.00   |
| SPCC      | SSD                | 64 GB  | 7       | 726   | 0     | 1.99   |
| OCZ       | ARC100             | 240 GB | 3       | 726   | 0     | 1.99   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 9       | 723   | 0     | 1.98   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 3       | 721   | 0     | 1.98   |
| Micron    | 5300_MTFDDAK1T9TDS | 1.9 TB | 2       | 720   | 0     | 1.98   |
| Corsair   | Force GT           | 120 GB | 5       | 1345  | 2     | 1.97   |
| SK hynix  | SC300 M.2 2280     | 128 GB | 3       | 714   | 0     | 1.96   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 7       | 710   | 0     | 1.95   |
| Kingston  | SM2280S3G2120G     | 120 GB | 4       | 708   | 0     | 1.94   |
| Samsung   | Portable SSD T5    | 1 TB   | 2       | 707   | 0     | 1.94   |
| China     | 120GB SATA Flas... | 120 GB | 4       | 706   | 0     | 1.94   |
| SanDisk   | SDSSDHII960G       | 960 GB | 3       | 705   | 0     | 1.93   |
| Lite-On   | LCS-256L9S-11 2... | 256 GB | 2       | 705   | 0     | 1.93   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 5       | 701   | 0     | 1.92   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 2       | 700   | 0     | 1.92   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 8       | 700   | 0     | 1.92   |
| Kingston  | SV300S37A480G      | 480 GB | 2       | 695   | 0     | 1.91   |
| KingSpec  | NT-32              | 32 GB  | 2       | 690   | 0     | 1.89   |
| SanDisk   | SSD U100           | 16 GB  | 10      | 689   | 0     | 1.89   |
| Kingston  | SM2280S3120G       | 120 GB | 4       | 687   | 0     | 1.88   |
| Seagate   | IronWolf ZA1000... | 1 TB   | 2       | 687   | 0     | 1.88   |
| Kingston  | SV300S37A240G      | 240 GB | 22      | 789   | 2     | 1.88   |
| ADATA     | SP600              | 64 GB  | 2       | 683   | 0     | 1.87   |
| Micron    | C400-MTFDDAK256MAM | 256 GB | 2       | 683   | 0     | 1.87   |
| SanDisk   | Ultra II           | 480 GB | 7       | 681   | 0     | 1.87   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 2       | 680   | 0     | 1.87   |
| HP        | SSD S700           | 1 TB   | 2       | 679   | 0     | 1.86   |
| Transcend | TS64GSSD340        | 64 GB  | 2       | 672   | 0     | 1.84   |
| SanDisk   | SSD PLUS 120 GB    | 120 GB | 6       | 912   | 1     | 1.84   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 2       | 671   | 0     | 1.84   |
| Samsung   | SSD 860 QVO        | 1 TB   | 24      | 671   | 0     | 1.84   |
| SanDisk   | SDSSDP128G         | 128 GB | 14      | 668   | 0     | 1.83   |
| Intel     | SSDSC2BX400G4      | 400 GB | 2       | 666   | 0     | 1.83   |
| SanDisk   | X400 M.2 2280      | 128 GB | 13      | 663   | 0     | 1.82   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 2       | 659   | 0     | 1.81   |
| Goodram   | SSDPR-CX400-128    | 128 GB | 3       | 657   | 0     | 1.80   |
| Apple     | SSD SM0256G        | 256 GB | 3       | 654   | 0     | 1.79   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 3       | 1383  | 4     | 1.79   |
| Apple     | SSD SM0512F        | 500 GB | 4       | 653   | 0     | 1.79   |
| Toshiba   | Q300               | 120 GB | 2       | 652   | 0     | 1.79   |
| Crucial   | CT128M550SSD1      | 128 GB | 3       | 1088  | 7     | 1.76   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 11      | 640   | 0     | 1.75   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 2       | 638   | 0     | 1.75   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 7       | 633   | 0     | 1.74   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 8       | 632   | 0     | 1.73   |
| OCZ       | VERTEX2            | 55 GB  | 2       | 630   | 0     | 1.73   |
| Samsung   | MZ7LN256HAJQ-000L7 | 256 GB | 4       | 627   | 0     | 1.72   |
| Wicgtyp   | M900-128           | 128 GB | 3       | 626   | 0     | 1.72   |
| OCZ       | TRION150           | 480 GB | 2       | 625   | 0     | 1.71   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 4       | 625   | 0     | 1.71   |
| Goodram   | SSD                | 120 GB | 8       | 624   | 0     | 1.71   |
| Kingston  | SMS100S232G        | 32 GB  | 2       | 624   | 0     | 1.71   |
| Crucial   | CT250MX500SSD4     | 250 GB | 6       | 623   | 0     | 1.71   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 3       | 623   | 0     | 1.71   |
| Kingston  | SUV400S37120G      | 120 GB | 29      | 739   | 88    | 1.71   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 4       | 620   | 0     | 1.70   |
| Samsung   | MZNLF128HCHP-000L1 | 128 GB | 2       | 619   | 0     | 1.70   |
| Intel     | SSDSC2CT120A3      | 120 GB | 12      | 1022  | 1     | 1.69   |
| SanDisk   | SD8SB8U-256G-1006  | 256 GB | 2       | 616   | 0     | 1.69   |
| Crucial   | CT960BX500SSD1     | 960 GB | 4       | 615   | 0     | 1.69   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 9       | 614   | 0     | 1.68   |
| Kingston  | SUV500MS120G       | 120 GB | 76      | 612   | 0     | 1.68   |
| China     | M10C               | 256 GB | 4       | 611   | 0     | 1.68   |
| Crucial   | CT1050MX300SSD4    | 1 TB   | 3       | 1524  | 4     | 1.67   |
| Hoodisk   | SSD                | 64 GB  | 71      | 610   | 0     | 1.67   |
| Innodisk  | mSATA 3TE7         | 32 GB  | 2       | 610   | 0     | 1.67   |
| Kingston  | SUV500120G         | 120 GB | 3       | 608   | 0     | 1.67   |
| Samsung   | SSD 860 QVO        | 2 TB   | 5       | 608   | 0     | 1.67   |
| ATP       | SATA III mSATA     | 120 GB | 12      | 606   | 0     | 1.66   |
| Intel     | SSDSC2BW180A4      | 180 GB | 22      | 637   | 1     | 1.66   |
| Intel     | SSDSC2KG480G8      | 480 GB | 8       | 701   | 1     | 1.66   |
| Apacer    | 128GB SATA Flas... | 128 GB | 6       | 601   | 0     | 1.65   |
| Seagate   | XA960LE10063       | 960 GB | 2       | 601   | 0     | 1.65   |
| SanDisk   | SSD U100           | 128 GB | 3       | 595   | 0     | 1.63   |
| Corsair   | Force GS           | 180 GB | 3       | 1289  | 2     | 1.63   |
| Intel     | SSDSC2KG480G8R     | 480 GB | 4       | 593   | 0     | 1.63   |
| Intenso   | JAJMS600M128G      | 128 GB | 2       | 591   | 0     | 1.62   |
| Indilinx  | IND-S3MP-256G      | 256 GB | 3       | 589   | 0     | 1.62   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 9       | 589   | 0     | 1.61   |
| Intenso   | JAJMS600M256G      | 256 GB | 5       | 588   | 0     | 1.61   |
| Intel     | SSDSC2BB012T7      | 1.2 TB | 2       | 1169  | 1     | 1.60   |
| Intel     | SSDMAEMC040G2      | 40 GB  | 3       | 793   | 1     | 1.59   |
| Hoodisk   | SSD                | 256 GB | 19      | 581   | 0     | 1.59   |
| Corsair   | Force 3 SSD        | 120 GB | 8       | 956   | 129   | 1.59   |
| Kston     | SSD                | 32 GB  | 6       | 578   | 0     | 1.59   |
| Advantech | SQF-SLMM2-8G-8SE   | 8 GB   | 3       | 577   | 0     | 1.58   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 5       | 577   | 0     | 1.58   |
| SanDisk   | X600 M.2 2280 SATA | 128 GB | 2       | 574   | 0     | 1.57   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 7       | 573   | 0     | 1.57   |
| TCSUNBOW  | M1                 | 32 GB  | 6       | 570   | 0     | 1.56   |
| China     | GM256              | 256 GB | 2       | 569   | 0     | 1.56   |
| Intenso   | SSD Sata III       | 120 GB | 6       | 568   | 0     | 1.56   |
| SanDisk   | SD8SN8U128G1001    | 128 GB | 2       | 564   | 0     | 1.55   |
| Samsung   | MZ7LN128HAHQ-000L2 | 128 GB | 2       | 563   | 0     | 1.54   |
| Intel     | SSDMCEAW120A4      | 120 GB | 6       | 562   | 0     | 1.54   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 5       | 562   | 0     | 1.54   |
| OWC       | Mercury Electra... | 240 GB | 6       | 562   | 0     | 1.54   |
| Innodisk  | DEMSR- 32GB mSA... | 32 GB  | 3       | 557   | 0     | 1.53   |
| Team      | T253X5480G         | 480 GB | 2       | 557   | 0     | 1.53   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 4       | 556   | 0     | 1.52   |
| SanDisk   | SDSSDHII120G       | 120 GB | 9       | 555   | 0     | 1.52   |
| Samsung   | SSD 840 Series     | 500 GB | 4       | 686   | 1     | 1.52   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 4       | 553   | 0     | 1.52   |
| Patriot   | Burst              | 480 GB | 2       | 552   | 0     | 1.51   |
| Kingston  | SS200S330G         | 32 GB  | 5       | 551   | 0     | 1.51   |
| VICK      | SSD 256G           | 256 GB | 2       | 548   | 0     | 1.50   |
| Intel     | SSDSC2CT240A4      | 240 GB | 3       | 834   | 2     | 1.50   |
| SK hynix  | SC311 SATA         | 128 GB | 14      | 548   | 0     | 1.50   |
| Transcend | TS128GSSD370S      | 128 GB | 4       | 545   | 0     | 1.49   |
| Kingston  | SV300S37A60G       | 64 GB  | 25      | 1089  | 36    | 1.49   |
| Phison    | SATA SSD           | 16 GB  | 45      | 544   | 0     | 1.49   |
| Intel     | SSDSC2KB240G8      | 240 GB | 24      | 543   | 0     | 1.49   |
| OCZ       | VERTEX3            | 240 GB | 2       | 1232  | 511   | 1.48   |
| Crucial   | CT525MX300SSD1     | 528 GB | 19      | 707   | 2     | 1.48   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 3       | 539   | 0     | 1.48   |
| Micron    | M500_MTFDDAK480MAV | 480 GB | 2       | 3117  | 5     | 1.46   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 3       | 534   | 0     | 1.46   |
| Transcend | TS128GSSD230S      | 128 GB | 7       | 531   | 0     | 1.46   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 2       | 530   | 0     | 1.45   |
| Lite-On   | CV8-CE128-11 SATA  | 128 GB | 3       | 528   | 0     | 1.45   |
| Samsung   | SSD 860 EVO        | 4 TB   | 2       | 527   | 0     | 1.45   |
| Kston     | SSD                | 64 GB  | 10      | 527   | 0     | 1.44   |
| SPCC      | SSD                | 1 TB   | 22      | 524   | 0     | 1.44   |
| China     | XJH-64GB           | 64 GB  | 2       | 524   | 0     | 1.44   |
| Samsung   | SSD 860 EVO        | 500 GB | 104     | 534   | 10    | 1.43   |
| Innodisk  | DEM24-32GM41BC1... | 32 GB  | 3       | 521   | 0     | 1.43   |
| Transcend | TS32GSSD340K       | 32 GB  | 2       | 518   | 0     | 1.42   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 3       | 516   | 0     | 1.42   |
| Kingston  | SMS200S3120G       | 120 GB | 17      | 1245  | 11    | 1.41   |
| Crucial   | CT250MX200SSD4     | 250 GB | 2       | 515   | 0     | 1.41   |
| Samsung   | MZYLF128HCHP-000L2 | 128 GB | 4       | 513   | 0     | 1.41   |
| Transcend | TS240GSSD220S      | 240 GB | 3       | 509   | 0     | 1.40   |
| Apacer    | 32GB SATA Flash... | 32 GB  | 24      | 627   | 52    | 1.39   |
| WDC       | WDBNCE2500PNC      | 250 GB | 4       | 505   | 0     | 1.39   |
| Intel     | SSDSC2BW240H6      | 240 GB | 5       | 504   | 0     | 1.38   |
| SanDisk   | SD9SB8W256G1122    | 256 GB | 2       | 504   | 0     | 1.38   |
| Crucial   | CT275MX300SSD4     | 275 GB | 6       | 772   | 34    | 1.38   |
| SanDisk   | X400 M.2 2280      | 256 GB | 7       | 502   | 0     | 1.38   |
| OCZ       | TRION100           | 240 GB | 3       | 502   | 0     | 1.38   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 4       | 500   | 0     | 1.37   |
| Smartbuy  | SSD                | 120 GB | 2       | 494   | 0     | 1.35   |
| SanDisk   | SDSSDA120G         | 120 GB | 42      | 496   | 18    | 1.35   |
| China     | SSD                | 64 GB  | 2       | 492   | 0     | 1.35   |
| SanDisk   | SD7SN3Q512G1002    | 512 GB | 2       | 491   | 0     | 1.35   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 8       | 1639  | 636   | 1.34   |
| Intel     | SSDSC2BW240A4      | 240 GB | 12      | 490   | 0     | 1.34   |
| SanDisk   | SD8TB8U512G1001    | 512 GB | 2       | 489   | 0     | 1.34   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 2       | 488   | 0     | 1.34   |
| Pccooler  | MSATA 128G         | 128 GB | 4       | 488   | 0     | 1.34   |
| Hoodisk   | SSD                | 128 GB | 79      | 487   | 0     | 1.34   |
| KingFast  | SSD                | 120 GB | 31      | 509   | 31    | 1.33   |
| WDC       | WDS500G1R0A-68A4W0 | 500 GB | 16      | 485   | 0     | 1.33   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 7       | 720   | 145   | 1.33   |
| SanDisk   | SSD i100           | 24 GB  | 2       | 484   | 0     | 1.33   |
| SK hynix  | SC311 SATA         | 256 GB | 14      | 483   | 0     | 1.32   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 2       | 482   | 0     | 1.32   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 18      | 481   | 0     | 1.32   |
| Apple     | SSD SM0512G        | 500 GB | 5       | 479   | 0     | 1.31   |
| Innodisk  | DEMSR- 16GB mSA... | 16 GB  | 10      | 479   | 0     | 1.31   |
| PNY       | CS1311 120GB SSD   | 120 GB | 6       | 536   | 1     | 1.31   |
| Gigaby... | GP-GSTFS31240GNTD  | 240 GB | 2       | 477   | 0     | 1.31   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 5       | 476   | 0     | 1.31   |
| Intel     | SSDSC2KW256G8      | 256 GB | 13      | 482   | 1     | 1.30   |
| SuperM... | SSD                | 16 GB  | 2       | 1243  | 506   | 1.30   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 2       | 472   | 0     | 1.29   |
| Samsung   | SSD 750 EVO        | 500 GB | 2       | 471   | 0     | 1.29   |
| Intel     | SSDSC2KG240G8      | 240 GB | 13      | 471   | 0     | 1.29   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 12      | 505   | 4     | 1.29   |
| Samsung   | MZ7L37T6HBLA-00A07 | 7.6 TB | 5       | 470   | 0     | 1.29   |
| Samsung   | MZ7LN128HCHP-00000 | 128 GB | 2       | 467   | 0     | 1.28   |
| Samsung   | MZNLN512HMJP-000L7 | 512 GB | 2       | 465   | 0     | 1.28   |
| Goodram   | SSDPR-CL100-120-G2 | 120 GB | 3       | 461   | 0     | 1.26   |
| Samsung   | SSD 860 EVO        | 250 GB | 99      | 460   | 0     | 1.26   |
| KingFast  | SSD                | 16 GB  | 6       | 458   | 0     | 1.26   |
| Apacer    | AS350              | 120 GB | 2       | 453   | 0     | 1.24   |
| Samsung   | SSD 650            | 120 GB | 3       | 450   | 0     | 1.23   |
| Samsung   | SSD 860 PRO        | 256 GB | 24      | 449   | 0     | 1.23   |
| OCZ       | SOLID3             | 64 GB  | 2       | 448   | 0     | 1.23   |
| Micron    | 5200_MTFDDAK1T9TDN | 1.9 TB | 2       | 446   | 0     | 1.22   |
| Lexar     | SSD                | 128 GB | 2       | 446   | 0     | 1.22   |
| Plextor   | PX-256M5Pro        | 256 GB | 2       | 445   | 0     | 1.22   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 7       | 509   | 1     | 1.22   |
| China     | SATA SSD           | 120 GB | 35      | 482   | 2     | 1.21   |
| Crucial   | CT512MX100SSD1     | 512 GB | 2       | 443   | 0     | 1.21   |
| Intel     | SSDSC2CW120A3      | 120 GB | 11      | 1786  | 648   | 1.21   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 4       | 441   | 0     | 1.21   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 11      | 440   | 0     | 1.21   |
| Crucial   | CT120BX500SSD1     | 120 GB | 61      | 440   | 0     | 1.21   |
| Crucial   | CT120BX300SSD1     | 120 GB | 5       | 439   | 0     | 1.20   |
| BR        | SSD                | 128 GB | 2       | 439   | 0     | 1.20   |
| SanDisk   | SSD PLUS           | 120 GB | 45      | 447   | 1     | 1.20   |
| Advantech | SQF-SM8M4-128G-SBC | 128 GB | 2       | 439   | 0     | 1.20   |
| Intel     | SSDSC2BP480G4      | 480 GB | 3       | 439   | 0     | 1.20   |
| Phison    | SATA SSD           | 128 GB | 5       | 438   | 0     | 1.20   |
| Intel     | SSDSCKKW256G8      | 256 GB | 3       | 436   | 0     | 1.20   |
| Samsung   | SSD 850            | 120 GB | 3       | 432   | 0     | 1.19   |
| Kingston  | SHFS37A240G        | 240 GB | 10      | 430   | 0     | 1.18   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 5       | 430   | 0     | 1.18   |
| Kingston  | SUV400S37480G      | 480 GB | 3       | 847   | 4     | 1.18   |
| Samsung   | 470 Series SSD     | 64 GB  | 3       | 431   | 1     | 1.18   |
| SanDisk   | SD9SN8W-256G-1006  | 256 GB | 2       | 426   | 0     | 1.17   |
| SK hynix  | SC308 SATA         | 256 GB | 6       | 727   | 14    | 1.17   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 15      | 564   | 2     | 1.16   |
| Intel     | SSDSA2BW160G3H     | 160 GB | 6       | 550   | 8     | 1.16   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 2       | 419   | 0     | 1.15   |
| SK hynix  | SHGS31-500GS-2     | 500 GB | 7       | 438   | 6     | 1.15   |
| Plextor   | PX-128M5S          | 128 GB | 4       | 662   | 1     | 1.15   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 13      | 1847  | 8     | 1.14   |
| Samsung   | MZ7LH480HAHQ-00005 | 480 GB | 2       | 417   | 0     | 1.14   |
| China     | SATA SSD           | 64 GB  | 20      | 482   | 6     | 1.14   |
| Team      | TEAML5Lite3D120G   | 120 GB | 3       | 414   | 0     | 1.14   |
| Patriot   | Burst              | 120 GB | 22      | 413   | 0     | 1.13   |
| Transcend | TS256GSSD420K      | 256 GB | 2       | 413   | 0     | 1.13   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 2       | 885   | 8     | 1.13   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 3       | 411   | 0     | 1.13   |
| SPCC      | SSD                | 120 GB | 15      | 417   | 1     | 1.12   |
| Samsung   | SSD 870 QVO        | 2 TB   | 20      | 409   | 0     | 1.12   |
| Transcend | TS120GMTS420S      | 120 GB | 21      | 409   | 0     | 1.12   |
| PNY       | CS900 120GB SSD    | 120 GB | 55      | 408   | 0     | 1.12   |
| SanDisk   | SD6SB1M-128G-1006  | 128 GB | 2       | 407   | 0     | 1.12   |
| MyDigi... | SB2                | 240 GB | 5       | 615   | 2     | 1.12   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 2       | 406   | 0     | 1.11   |
| SanDisk   | SDSSDH3 1T02       | 1 TB   | 2       | 406   | 0     | 1.11   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 12      | 405   | 0     | 1.11   |
| Kingston  | SVP200S37A120G     | 120 GB | 3       | 996   | 2     | 1.10   |
| SanDisk   | X400 M.2 2280      | 512 GB | 3       | 400   | 0     | 1.10   |
| Toshiba   | TR200              | 240 GB | 9       | 399   | 0     | 1.09   |
| Apple     | SSD TS256C         | 256 GB | 2       | 566   | 4     | 1.09   |

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
| HPE         | 6      | 12      | 1484  | 0     | 4.07   |
| Kingmax     | 1      | 2       | 1341  | 0     | 3.68   |
| Dell        | 1      | 2       | 1173  | 0     | 3.22   |
| OCZ         | 22     | 90      | 1259  | 37    | 2.89   |
| GAMER       | 1      | 2       | 970   | 0     | 2.66   |
| Mushkin     | 5      | 16      | 919   | 0     | 2.52   |
| Corsair     | 10     | 42      | 1171  | 121   | 2.46   |
| HP          | 12     | 31      | 1034  | 1     | 2.40   |
| Intel       | 99     | 556     | 1025  | 56    | 2.25   |
| Indilinx    | 3      | 7       | 787   | 0     | 2.16   |
| Samsung     | 156    | 1799    | 735   | 9     | 1.91   |
| Seagate     | 10     | 22      | 672   | 0     | 1.84   |
| Hoodisk     | 6      | 274     | 616   | 0     | 1.69   |
| Apple       | 12     | 44      | 645   | 18    | 1.65   |
| SuperMicro  | 4      | 13      | 697   | 78    | 1.59   |
| Toshiba     | 22     | 72      | 654   | 14    | 1.58   |
| TCSUNBOW    | 1      | 6       | 570   | 0     | 1.56   |
| Micron      | 36     | 152     | 733   | 83    | 1.52   |
| VICK        | 1      | 2       | 548   | 0     | 1.50   |
| SanDisk     | 115    | 634     | 527   | 10    | 1.35   |
| Pccooler    | 1      | 4       | 488   | 0     | 1.34   |
| Phison      | 7      | 70      | 474   | 1     | 1.28   |
| ADATA       | 39     | 299     | 490   | 29    | 1.25   |
| Kston       | 4      | 30      | 442   | 1     | 1.19   |
| Crucial     | 45     | 709     | 507   | 26    | 1.18   |
| Advantech   | 3      | 7       | 429   | 0     | 1.18   |
| Goodram     | 13     | 57      | 419   | 0     | 1.15   |
| Kingston    | 63     | 1165    | 493   | 18    | 1.14   |
| MyDigita... | 1      | 5       | 615   | 2     | 1.12   |
| Pioneer     | 3      | 6       | 405   | 0     | 1.11   |
| PNY         | 14     | 142     | 390   | 1     | 1.06   |
| Innodisk    | 11     | 74      | 380   | 0     | 1.04   |
| SK hynix    | 19     | 100     | 499   | 45    | 1.03   |
| Neo Forza   | 1      | 2       | 376   | 0     | 1.03   |
| Integral    | 1      | 5       | 353   | 0     | 0.97   |
| Apacer      | 13     | 114     | 446   | 19    | 0.96   |
| BIWIN       | 2      | 42      | 361   | 7     | 0.93   |
| OWC         | 3      | 15      | 338   | 0     | 0.93   |
| China       | 61     | 566     | 357   | 4     | 0.93   |
| KingFast    | 9      | 65      | 384   | 16    | 0.92   |
| WDC         | 34     | 375     | 349   | 9     | 0.90   |
| AMD         | 3      | 12      | 334   | 2     | 0.84   |
| BORY        | 1      | 10      | 286   | 0     | 0.79   |
| ATP         | 5      | 26      | 284   | 0     | 0.78   |
| Gigabyte    | 4      | 34      | 283   | 0     | 0.78   |
| Patriot     | 14     | 88      | 334   | 36    | 0.77   |
| Inland      | 1      | 2       | 273   | 0     | 0.75   |
| Protectli   | 11     | 135     | 267   | 0     | 0.73   |
| minisforum  | 2      | 18      | 248   | 0     | 0.68   |
| EMTEC       | 2      | 8       | 248   | 0     | 0.68   |
| Smartbuy    | 3      | 6       | 235   | 0     | 0.65   |
| SHAREVDI    | 1      | 22      | 235   | 0     | 0.65   |
| Intenso     | 14     | 103     | 237   | 1     | 0.63   |
| MidasForce  | 2      | 5       | 230   | 0     | 0.63   |
| Wintec      | 1      | 3       | 228   | 0     | 0.62   |
| Plextor     | 7      | 18      | 323   | 3     | 0.62   |
| SPCC        | 12     | 175     | 235   | 2     | 0.61   |
| Gigabyte... | 3      | 13      | 219   | 0     | 0.60   |
| SATADOM     | 2      | 11      | 216   | 0     | 0.59   |
| Wicgtyp     | 3      | 16      | 214   | 0     | 0.59   |
| FORESEE     | 5      | 133     | 211   | 0     | 0.58   |
| Leven       | 4      | 9       | 246   | 1     | 0.57   |
| Dogfish     | 6      | 61      | 212   | 1     | 0.57   |
| Team        | 10     | 34      | 203   | 0     | 0.56   |
| Transcend   | 62     | 582     | 199   | 2     | 0.54   |
| Lite-On     | 22     | 58      | 199   | 60    | 0.52   |
| SUNEAST     | 1      | 2       | 290   | 15    | 0.51   |
| Lenovo      | 1      | 2       | 185   | 0     | 0.51   |
| Zheino      | 3      | 6       | 175   | 0     | 0.48   |
| KIOXIA-E... | 2      | 8       | 174   | 0     | 0.48   |
| Wibtek      | 1      | 2       | 172   | 0     | 0.47   |
| BR          | 3      | 6       | 155   | 0     | 0.42   |
| Qunion      | 1      | 2       | 155   | 1     | 0.40   |
| Vaseky      | 4      | 9       | 146   | 0     | 0.40   |
| KeepData    | 1      | 18      | 150   | 1     | 0.39   |
| KingSpec    | 17     | 64      | 153   | 17    | 0.39   |
| ShiJi       | 5      | 35      | 147   | 2     | 0.37   |
| Lexar       | 5      | 25      | 133   | 0     | 0.37   |
| CWDISK      | 2      | 7       | 126   | 0     | 0.35   |
| ZTC         | 1      | 2       | 640   | 14    | 0.34   |
| Silicon     | 1      | 2       | 114   | 0     | 0.31   |
| VICKTER     | 4      | 15      | 113   | 0     | 0.31   |
| AirDisk     | 2      | 17      | 112   | 0     | 0.31   |
| Drevo       | 1      | 4       | 111   | 0     | 0.31   |
| KingDian    | 3      | 9       | 144   | 146   | 0.29   |
| Verbatim    | 3      | 24      | 94    | 0     | 0.26   |
| GOFATOO     | 3      | 18      | 91    | 0     | 0.25   |
| Faspeed     | 1      | 4       | 90    | 0     | 0.25   |
| ORICO       | 3      | 6       | 87    | 0     | 0.24   |
| Supermicro  | 1      | 2       | 87    | 0     | 0.24   |
| UDinfo      | 1      | 3       | 82    | 0     | 0.23   |
| BAITITON    | 2      | 10      | 96    | 1     | 0.22   |
| SCY         | 1      | 2       | 77    | 0     | 0.21   |
| Kimtigo     | 1      | 4       | 72    | 0     | 0.20   |
| Netac       | 8      | 28      | 73    | 6     | 0.18   |
| LuminouTek  | 1      | 2       | 64    | 0     | 0.18   |
| Fanxiang    | 1      | 2       | 413   | 3     | 0.16   |
| LDLC        | 1      | 2       | 62    | 1516  | 0.16   |
| Yeyian      | 1      | 2       | 56    | 0     | 0.15   |
| XUM         | 1      | 3       | 47    | 0     | 0.13   |
| T-FORCE     | 4      | 13      | 46    | 0     | 0.13   |
| Kingchuxing | 1      | 3       | 41    | 0     | 0.11   |
| Colorful    | 1      | 2       | 41    | 0     | 0.11   |
| HUGWORLD    | 2      | 4       | 39    | 0     | 0.11   |
| XrayDisk    | 2      | 4       | 52    | 6     | 0.09   |
| Hikvision   | 3      | 6       | 21    | 0     | 0.06   |
| HCiPC       | 1      | 2       | 20    | 0     | 0.06   |
| FIKWOT      | 1      | 2       | 58    | 13    | 0.05   |
| KUU         | 1      | 2       | 19    | 0     | 0.05   |
| Kingsand    | 1      | 4       | 17    | 0     | 0.05   |
| SSSTC       | 2      | 6       | 28    | 672   | 0.02   |
| MEMXPRO     | 1      | 4       | 5     | 0     | 0.02   |
| Valuetech   | 1      | 2       | 5     | 0     | 0.02   |
| Fordisk     | 1      | 4       | 4     | 0     | 0.01   |
| INDMEM      | 2      | 4       | 45    | 8     | 0.01   |
| HOGE        | 1      | 2       | 2     | 0     | 0.01   |
| SCWLF       | 1      | 2       | 1     | 0     | 0.00   |
| Timetec     | 1      | 2       | 1     | 0     | 0.00   |
| VisionTek   | 1      | 3       | 1072  | 1019  | 0.00   |
| Dahua       | 1      | 2       | 0     | 0     | 0.00   |
| HP Phison   | 2      | 4       | 510   | 1037  | 0.00   |

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
| Samsung   | SSD 950 PRO        | 512 GB | 3       | 1522  | 0     | 4.17   |
| Intel     | SSDPEDMW400G4      | 400 GB | 2       | 1410  | 0     | 3.86   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 2       | 1246  | 0     | 3.42   |
| Samsung   | SSD 950 PRO        | 256 GB | 3       | 1555  | 1     | 3.30   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 3       | 1141  | 0     | 3.13   |
| Intel     | SSDPE2MX450G7      | 450 GB | 2       | 1077  | 0     | 2.95   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 3       | 1053  | 0     | 2.89   |
| Intel     | SSDPEDKX040T7      | 4 TB   | 2       | 998   | 0     | 2.74   |
| Intel     | SSDPED1D280GA      | 280 GB | 3       | 887   | 0     | 2.43   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 4       | 871   | 0     | 2.39   |
| SK hynix  | PC601 NVMe         | 256 GB | 2       | 805   | 0     | 2.21   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 2       | 804   | 0     | 2.20   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 2       | 766   | 0     | 2.10   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 2       | 765   | 0     | 2.10   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 5       | 744   | 0     | 2.04   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 2       | 735   | 0     | 2.02   |
| SPCC      | M.2 PCIE SSD       | 512 GB | 2       | 723   | 0     | 1.98   |
| HP        | SSD EX920          | 256 GB | 2       | 709   | 0     | 1.94   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 4       | 689   | 0     | 1.89   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 8       | 658   | 0     | 1.81   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 5       | 649   | 0     | 1.78   |
| Toshiba   | THNSN51T02DUK NVMe | 1 TB   | 2       | 646   | 0     | 1.77   |
| Intel     | SSDPE21D280GA      | 280 GB | 3       | 627   | 0     | 1.72   |
| Samsung   | SSD 960 EVO        | 1 TB   | 4       | 640   | 1     | 1.68   |
| Samsung   | PM951 NVMe         | 256 GB | 5       | 610   | 0     | 1.67   |
| Samsung   | MZVPV256HDGL-00000 | 256 GB | 3       | 590   | 0     | 1.62   |
| Toshiba   | KBG30ZMS256G NVMe  | 256 GB | 2       | 578   | 0     | 1.59   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 4       | 565   | 0     | 1.55   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 3       | 561   | 0     | 1.54   |
| SK hynix  | SHGP31-1000GM      | 1 TB   | 3       | 554   | 0     | 1.52   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 10      | 546   | 0     | 1.50   |
| Intel     | SSDPEKKW128G8      | 128 GB | 3       | 544   | 0     | 1.49   |
| WDC       | PC SN730 NVMe      | 512 GB | 3       | 543   | 0     | 1.49   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 2       | 513   | 0     | 1.41   |
| Intel     | SSDPEKKW256G8      | 256 GB | 5       | 500   | 0     | 1.37   |
| Team      | TM8FP6128G         | 128 GB | 2       | 500   | 0     | 1.37   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 3       | 493   | 0     | 1.35   |
| Samsung   | PM961 NVMe         | 256 GB | 5       | 487   | 0     | 1.34   |
| HP        | SSD EX900          | 120 GB | 4       | 472   | 0     | 1.30   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 2       | 471   | 0     | 1.29   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 5       | 462   | 0     | 1.27   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 2       | 453   | 0     | 1.24   |
| Intel     | SSDPEKKW128G7      | 128 GB | 2       | 906   | 1     | 1.24   |
| Samsung   | SSD 970 PRO        | 512 GB | 19      | 445   | 0     | 1.22   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 12      | 445   | 0     | 1.22   |
| Samsung   | SSD 960 EVO        | 500 GB | 15      | 442   | 0     | 1.21   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 3       | 438   | 0     | 1.20   |
| Kingston  | SEDC1000BM8480G    | 480 GB | 2       | 434   | 0     | 1.19   |
| Samsung   | SSD 960 PRO        | 512 GB | 7       | 511   | 1     | 1.18   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 2       | 429   | 0     | 1.18   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 2       | 425   | 0     | 1.17   |
| SK hynix  | PC611 NVMe         | 512 GB | 2       | 423   | 0     | 1.16   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 9       | 418   | 0     | 1.15   |
| Samsung   | SSD 960 EVO        | 250 GB | 35      | 416   | 0     | 1.14   |
| Seagate   | BarraCuda Q5 ZP... | 500 GB | 2       | 412   | 0     | 1.13   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 5       | 405   | 0     | 1.11   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 3       | 403   | 0     | 1.11   |
| ADATA     | SX8200PNP          | 512 GB | 9       | 443   | 1     | 1.10   |
| Micron    | 7450_MTFDKCC1T9TFR |        | 2       | 395   | 0     | 1.08   |
| Phison    | Sabrent            | 1 TB   | 24      | 390   | 0     | 1.07   |
| Corsair   | Force MP600        | 1 TB   | 2       | 388   | 0     | 1.06   |
| Kingston  | SA1000M8240G       | 240 GB | 3       | 387   | 0     | 1.06   |
| WDC       | PC SN520 SDAPNU... |        | 4       | 387   | 0     | 1.06   |
| Gigaby... | GP-AG42TB          | 2 TB   | 2       | 385   | 0     | 1.06   |
| Samsung   | MZVLQ128HBHQ-000H1 | 128 GB | 2       | 382   | 0     | 1.05   |
| HP        | SSD EX920          | 512 GB | 2       | 379   | 0     | 1.04   |
| Intel     | SSDPEKKW512G7      | 512 GB | 3       | 726   | 1     | 1.04   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 27      | 378   | 0     | 1.04   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 5       | 375   | 0     | 1.03   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 5       | 375   | 0     | 1.03   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 10      | 374   | 0     | 1.03   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 3       | 364   | 0     | 1.00   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 2       | 363   | 0     | 0.99   |
| Samsung   | MZQL23T8HCLS-00A07 |        | 2       | 361   | 0     | 0.99   |
| KIOXIA... | SSD                | 500 GB | 5       | 348   | 0     | 0.95   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 2       | 345   | 0     | 0.95   |
| Plextor   | PX-256M8PeG        | 256 GB | 3       | 390   | 69    | 0.93   |
| Dell      | Express Flash N... | 375 GB | 2       | 336   | 0     | 0.92   |
| Corsair   | Force MP600        | 2 TB   | 2       | 336   | 0     | 0.92   |
| Timetec   | 35TTFP6PCIE-256G   | 256 GB | 2       | 335   | 0     | 0.92   |
| Silico... | 512GB PCS PCIe ... | 512 GB | 2       | 333   | 0     | 0.91   |
| Samsung   | MZVLW256HEHP-00000 | 256 GB | 2       | 328   | 0     | 0.90   |
| Corsair   | Force MP510        | 240 GB | 4       | 326   | 0     | 0.89   |
| Crucial   | CT500P1SSD8        | 500 GB | 13      | 326   | 0     | 0.89   |
| WDC       | WDS100T1X0E-00AFY0 | 1 TB   | 5       | 325   | 0     | 0.89   |
| ADATA     | SX6000NP           | 128 GB | 2       | 325   | 0     | 0.89   |
| ADATA     | SX8200PNP          | 1 TB   | 11      | 334   | 5     | 0.88   |
| Kingston  | SEDC1000BM8240G    | 240 GB | 5       | 319   | 0     | 0.87   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 4       | 318   | 0     | 0.87   |
| Lexar     | 256GB SSD          | 256 GB | 9       | 317   | 0     | 0.87   |
| ADATA     | SX8200PNP          | 256 GB | 8       | 315   | 0     | 0.86   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 4       | 314   | 0     | 0.86   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 2       | 311   | 0     | 0.85   |
| Transcend | TS128GMTE110S      | 128 GB | 24      | 311   | 0     | 0.85   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 12      | 329   | 1     | 0.85   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 6       | 309   | 0     | 0.85   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 10      | 307   | 0     | 0.84   |
| Kingston  | SA2000M81000G      | 1 TB   | 7       | 314   | 145   | 0.83   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 4       | 298   | 0     | 0.82   |
| WDC       | PC SN520 NVMe      | 512 GB | 2       | 297   | 0     | 0.81   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 13      | 296   | 0     | 0.81   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 19      | 296   | 0     | 0.81   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 45      | 296   | 0     | 0.81   |
| Corsair   | Force MP600        | 500 GB | 3       | 292   | 0     | 0.80   |
| PNY       | CS1030 250GB SSD   | 250 GB | 3       | 289   | 0     | 0.79   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 4       | 288   | 0     | 0.79   |
| Kingston  | SA2000M8500G       | 500 GB | 12      | 287   | 0     | 0.79   |
| Samsung   | MZVLW512HMJP-000L7 | 512 GB | 3       | 283   | 0     | 0.78   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 2       | 279   | 0     | 0.77   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 7       | 274   | 0     | 0.75   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 22      | 273   | 0     | 0.75   |
| Micron    | 7300_MTFDHBA400TDG | 400 GB | 2       | 272   | 0     | 0.75   |
| Phison    | Viper M.2 VPN100   | 1 TB   | 2       | 265   | 0     | 0.73   |
| Samsung   | SSD 970 EVO        | 250 GB | 17      | 357   | 2     | 0.72   |
| Intel     | SSDPEKNW512G8      | 512 GB | 15      | 261   | 0     | 0.72   |
| Corsair   | Force MP300        | 120 GB | 2       | 257   | 0     | 0.71   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 4       | 256   | 0     | 0.70   |
| KIOXIA... | G2 SSD             | 500 GB | 2       | 255   | 0     | 0.70   |
| Samsung   | MZVLW256HEHP-000L7 |        | 23      | 251   | 0     | 0.69   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 3       | 249   | 0     | 0.68   |
| minisf... | 512GB              | 512 GB | 2       | 246   | 0     | 0.68   |
| Samsung   | SSD 970 PRO        | 1 TB   | 9       | 241   | 0     | 0.66   |
| Kingston  | SKC2500M8250G      | 250 GB | 3       | 239   | 0     | 0.66   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 7       | 239   | 0     | 0.66   |
| Samsung   | SSD 980            | 250 GB | 17      | 237   | 0     | 0.65   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 2       | 236   | 0     | 0.65   |
| WDC       | WDS240G2G0C-00AJM0 | 240 GB | 3       | 234   | 0     | 0.64   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 8       | 233   | 0     | 0.64   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 17      | 240   | 12    | 0.63   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 8       | 228   | 0     | 0.63   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 3       | 224   | 0     | 0.61   |
| Acer      | SSD FA100          | 256 GB | 3       | 222   | 0     | 0.61   |
| Transcend | TS500GMTE240S      | 500 GB | 2       | 214   | 0     | 0.59   |
| Seagate   | FireCuda 520 SS... | 500 GB | 7       | 213   | 0     | 0.59   |
| Gigabyte  | GP-GSM2NE3128GNTD  | 128 GB | 5       | 213   | 0     | 0.58   |
| Transcend | TS256GMTE110S      | 256 GB | 5       | 212   | 0     | 0.58   |
| PNY       | CS3030 500GB SSD   | 500 GB | 3       | 212   | 0     | 0.58   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 8       | 209   | 0     | 0.57   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 3       | 208   | 0     | 0.57   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 6       | 206   | 0     | 0.57   |
| FORESEE   | P900F128GBH        | 128 GB | 2       | 206   | 0     | 0.57   |
| Samsung   | MZVL2256HCHQ-00B00 | 256 GB | 2       | 408   | 1     | 0.56   |
| Toshiba   | KXG6AZNV256G       | 256 GB | 2       | 204   | 0     | 0.56   |
| Samsung   | MZVLQ256HBJD-00BH1 | 256 GB | 2       | 203   | 0     | 0.56   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 3       | 200   | 0     | 0.55   |
| HGST      | HUSMR7632BDP301    |        | 2       | 199   | 0     | 0.55   |
| Samsung   | PM981 NVMe         | 256 GB | 7       | 197   | 0     | 0.54   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 3       | 195   | 0     | 0.54   |
| WDC       | PC SN730 NVMe      | 1 TB   | 2       | 194   | 0     | 0.53   |
| Silico... | 128GB              | 128 GB | 4       | 193   | 0     | 0.53   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 7       | 193   | 0     | 0.53   |
| ADATA     | SX6000LNP          | 128 GB | 2       | 192   | 0     | 0.53   |
| Samsung   | SSD 970 EVO        | 1 TB   | 19      | 216   | 1     | 0.53   |
| Intel     | HBRPEKNX0101AH     | 256 GB | 2       | 192   | 0     | 0.53   |
| KIOXIA    | KBG40ZNS256G NVMe  |        | 8       | 192   | 0     | 0.53   |
| Silico... | 512GB              | 512 GB | 2       | 188   | 0     | 0.52   |
| Transcend | TS256GMTE652T2     | 256 GB | 23      | 188   | 0     | 0.52   |
| HP        | SSD EX900          | 250 GB | 6       | 188   | 0     | 0.52   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 4       | 187   | 0     | 0.51   |
| SSSTC     | CL1-4D256          | 256 GB | 2       | 182   | 0     | 0.50   |
| SK hynix  | PC300 NVMe         | 256 GB | 2       | 182   | 0     | 0.50   |
| WDC       | PC SN520 NVMe      | 256 GB | 3       | 182   | 0     | 0.50   |
| Team      | TM8FPD512G         | 512 GB | 3       | 181   | 0     | 0.50   |
| Crucial   | CT500P5PSSD8       | 500 GB | 4       | 180   | 0     | 0.50   |
| Kingston  | OM8PDP3512B-A01    | 512 GB | 10      | 180   | 0     | 0.49   |
| Phison    | PCIe SSD           | 250 GB | 27      | 178   | 0     | 0.49   |
| Phison    | Sabrent Rocket 4.0 | 500 GB | 4       | 178   | 0     | 0.49   |
| Netac     | NVMe SSD           | 256 GB | 2       | 178   | 0     | 0.49   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 6       | 175   | 0     | 0.48   |
| Fanxiang  | S500               | 256 GB | 2       | 175   | 0     | 0.48   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 4       | 173   | 0     | 0.48   |
| WDC       | WDS500G1X0E-00AFY0 | 500 GB | 4       | 171   | 0     | 0.47   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 13      | 169   | 0     | 0.47   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 69      | 168   | 0     | 0.46   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 65      | 167   | 0     | 0.46   |
| Kingston  | OM8PCP3512F-AI1    | 512 GB | 3       | 166   | 0     | 0.46   |
| SK hynix  | SKHynix_HFM256G... | 256 GB | 3       | 164   | 0     | 0.45   |
| Crucial   | CT2000P3PSSD8      | 2 TB   | 3       | 164   | 0     | 0.45   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 2       | 163   | 0     | 0.45   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 2       | 162   | 0     | 0.45   |
| Samsung   | SSD 970 EVO        | 500 GB | 30      | 188   | 9     | 0.44   |
| KIOXIA    | KBG5AZNV256G LA    | 256 GB | 2       | 161   | 0     | 0.44   |
| Goodram   | SSDPR-PX500-256-80 | 256 GB | 3       | 160   | 0     | 0.44   |
| Kingston  | SNVS500G           | 500 GB | 11      | 157   | 0     | 0.43   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 2       | 157   | 0     | 0.43   |
| SanDisk   | WD Blue SN570      | 250 GB | 10      | 157   | 0     | 0.43   |
| EDILOCA   | EN605              | 256 GB | 2       | 156   | 0     | 0.43   |
| Lexar     | SSD                | 256 GB | 3       | 156   | 0     | 0.43   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 7       | 155   | 0     | 0.43   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 2       | 154   | 0     | 0.42   |
| Fanxiang  | S500PRO            | 256 GB | 10      | 154   | 0     | 0.42   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 8       | 153   | 0     | 0.42   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 6       | 150   | 0     | 0.41   |
| UMIS      | RPJTJ256MEE1OWX    | 256 GB | 2       | 147   | 0     | 0.41   |
| SK hynix  | SHGP31-500GM-2     | 500 GB | 5       | 147   | 0     | 0.41   |
| Samsung   | PM991 NVMe         | 256 GB | 6       | 146   | 0     | 0.40   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 7       | 157   | 1     | 0.40   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 7       | 145   | 0     | 0.40   |
| Kingston  | SA2000M8250G       | 250 GB | 17      | 144   | 0     | 0.40   |
| Kimtigo   | SSD                | 128 GB | 8       | 144   | 0     | 0.40   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 4       | 144   | 0     | 0.40   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 13      | 143   | 0     | 0.39   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 12      | 142   | 0     | 0.39   |
| Team      | TM8FP6512G         | 512 GB | 5       | 141   | 0     | 0.39   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 3       | 139   | 0     | 0.38   |
| Samsung   | MZVLQ256HAJD-000H1 | 256 GB | 5       | 137   | 0     | 0.38   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 7       | 137   | 0     | 0.38   |
| Silico... | NE-256             | 256 GB | 5       | 135   | 0     | 0.37   |
| LDLC      | F8+M.2 240         | 240 GB | 2       | 134   | 0     | 0.37   |
| SanDisk   | WD_BLACK SN770     | 250 GB | 4       | 134   | 0     | 0.37   |
| Micron    | 2200S NVMe         | 256 GB | 5       | 186   | 16    | 0.36   |
| Patriot   | M.2 P310           | 240 GB | 5       | 131   | 0     | 0.36   |
| WDC       | WDBRPG0010BNC-WRSN | 1 TB   | 2       | 131   | 0     | 0.36   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 3       | 131   | 0     | 0.36   |
| Silico... | GV128              | 128 GB | 11      | 130   | 0     | 0.36   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 25      | 136   | 1     | 0.36   |
| Samsung   | MZVLB256HBHQ-000H1 | 256 GB | 4       | 129   | 0     | 0.35   |
| Gigabyte  | GP-GSM2NE3256GNTD  |        | 11      | 128   | 0     | 0.35   |
| WDC       | WD BLACK SDBPNT... | 256 GB | 2       | 128   | 0     | 0.35   |
| KIOXIA    | KXG60ZNV256G       | 256 GB | 4       | 128   | 0     | 0.35   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 11      | 127   | 0     | 0.35   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 2       | 127   | 0     | 0.35   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 4       | 126   | 0     | 0.35   |
| Kingston  | SNV2S2000G         | 2 TB   | 3       | 125   | 0     | 0.34   |
| Micron    | 2300 NVMe          | 1 TB   | 2       | 124   | 0     | 0.34   |
| Crucial   | CT500P5SSD8        | 500 GB | 5       | 122   | 0     | 0.34   |
| Corsair   | Force MP510        | 480 GB | 4       | 122   | 0     | 0.34   |
| ORTIAL    | SSD                | 128 GB | 2       | 122   | 0     | 0.34   |
| SanDisk   | WD Red SN700       | 250 GB | 5       | 121   | 0     | 0.33   |
| SK hynix  | PC711 NVMe         | 256 GB | 2       | 119   | 0     | 0.33   |
| KIOXIA    | KBG50ZNS256G NVMe  | 256 GB | 4       | 117   | 0     | 0.32   |
| Samsung   | SSD 980 PRO        | 250 GB | 10      | 116   | 0     | 0.32   |
| Samsung   | Portable SSD T7    | 2 TB   | 2       | 116   | 0     | 0.32   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 2       | 116   | 0     | 0.32   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 5       | 115   | 0     | 0.32   |
| ATP       | NVMe M.2 2280 SSD  | 240 GB | 8       | 115   | 0     | 0.32   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 6       | 114   | 0     | 0.31   |
| Crucial   | CT250P2SSD8        | 250 GB | 17      | 113   | 0     | 0.31   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 3       | 113   | 0     | 0.31   |
| Micron    | 2300_MTFDHBA512TDV | 512 GB | 2       | 113   | 0     | 0.31   |
| Kingston  | SNVS250G           | 250 GB | 6       | 111   | 0     | 0.31   |
| Samsung   | 980 PRO with He... | 2 TB   | 2       | 110   | 0     | 0.30   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 17      | 127   | 60    | 0.30   |
| Team      | TM8FP6256G         | 256 GB | 17      | 107   | 0     | 0.29   |
| Fanxiang  | S501               | 512 GB | 3       | 106   | 0     | 0.29   |
| SPCC      | M.2 PCIe SSD       | 128 GB | 9       | 105   | 0     | 0.29   |
| Crucial   | CT500P2SSD8        | 500 GB | 19      | 105   | 0     | 0.29   |
| SanDisk   | WD_BLACK SN770     | 500 GB | 12      | 104   | 0     | 0.29   |
| Crucial   | CT1000P5PSSD8      | 1 TB   | 2       | 103   | 0     | 0.28   |
| Samsung   | SSD 970 EVO        | 2 TB   | 2       | 364   | 130   | 0.28   |
| KIOXIA    | KBG40ZNS128G NVMe  | 128 GB | 3       | 102   | 0     | 0.28   |
| Samsung   | SSD 980 PRO        | 500 GB | 32      | 102   | 0     | 0.28   |
| SPCC      | M.2 PCIe SSD       | 2 TB   | 2       | 102   | 0     | 0.28   |
| HP        | SSD EX950          | 512 GB | 10      | 102   | 0     | 0.28   |
| Crucial   | CT2000P3SSD8       | 2 TB   | 5       | 101   | 0     | 0.28   |
| Lexar     | 512GB SSD          | 512 GB | 2       | 101   | 0     | 0.28   |
| Intel     | SSDPEK1A058GA      | 64 GB  | 5       | 99    | 0     | 0.27   |
| SK hynix  | BC511 NVMe         | 256 GB | 3       | 99    | 0     | 0.27   |
| Silico... | BKHD Nvme 128G     | 128 GB | 4       | 99    | 0     | 0.27   |
| WDC       | PC SN730 SDBQNT... |        | 8       | 98    | 0     | 0.27   |
| Toshiba   | KBG40ZNT512G ME... | 512 GB | 4       | 98    | 0     | 0.27   |
| Kingston  | RBUSNS8154P3256GJ3 | 256 GB | 2       | 98    | 0     | 0.27   |
| Crucial   | CT2000P2SSD8       | 2 TB   | 3       | 97    | 0     | 0.27   |
| Micron    | 2300 NVMe          | 512 GB | 3       | 96    | 0     | 0.27   |
| Samsung   | SSD 980            | 500 GB | 40      | 101   | 1     | 0.26   |
| Kingston  | SA1000M8480G       | 480 GB | 2       | 94    | 0     | 0.26   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 4       | 94    | 0     | 0.26   |
| Samsung   | MZALQ512HBLU-00BL2 | 512 GB | 5       | 92    | 0     | 0.25   |
| Micron    | 2200S NVMe         | 1 TB   | 3       | 92    | 0     | 0.25   |
| Samsung   | MZVLB256HBHQ-000L2 | 256 GB | 4       | 91    | 0     | 0.25   |
| Samsung   | MZALQ128HBHQ-000L1 | 128 GB | 8       | 90    | 0     | 0.25   |
| SanDisk   | Ultra 3D NVMe      | 500 GB | 2       | 89    | 0     | 0.25   |
| SK hynix  | BC511 HFM256GDJ... | 256 GB | 6       | 89    | 0     | 0.25   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 7       | 89    | 0     | 0.25   |
| Samsung   | MZVLQ512HBLU-00B00 | 512 GB | 2       | 89    | 0     | 0.25   |
| Patriot   | M.2 P300           | 512 GB | 2       | 89    | 0     | 0.25   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 3       | 89    | 0     | 0.24   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 2       | 89    | 0     | 0.24   |
| Team      | TM8FP4001T         | 1 TB   | 3       | 88    | 0     | 0.24   |
| Micron    | MTFDHBA256TDV      | 256 GB | 2       | 87    | 0     | 0.24   |
| SK hynix  | SHGP31-500GM       | 500 GB | 5       | 86    | 0     | 0.24   |
| Samsung   | MZVLB512HBJQ-000H1 | 512 GB | 3       | 85    | 0     | 0.23   |
| Samsung   | MZALQ512HALU-000L2 | 512 GB | 3       | 85    | 0     | 0.23   |
| SanDisk   | WD Blue SN570      | 500 GB | 27      | 83    | 0     | 0.23   |
| Kingston  | SNV2S250G          | 250 GB | 15      | 83    | 0     | 0.23   |
| Phison    | 311CD0512GB        | 512 GB | 2       | 82    | 0     | 0.22   |
| Samsung   | MZALQ256HBJD-00BL2 | 256 GB | 6       | 80    | 0     | 0.22   |
| Transcend | TS256GMTE710T      | 256 GB | 25      | 79    | 0     | 0.22   |
| Micron    | 2450_EEFDKBA256TFK | 256 GB | 2       | 79    | 0     | 0.22   |
| China     | 512GB SSD          | 512 GB | 44      | 79    | 1     | 0.22   |
| Samsung   | PM9A1 NVMe         | 512 GB | 6       | 78    | 0     | 0.22   |
| Toshiba   | KBG40ZMT128G ME... |        | 3       | 77    | 0     | 0.21   |
| Samsung   | SSD 980            | 1 TB   | 34      | 76    | 0     | 0.21   |
| Crucial   | CT500P3PSSD8       | 500 GB | 8       | 75    | 0     | 0.21   |
| Netac     | NVMe SSD           | 128 GB | 3       | 75    | 0     | 0.21   |
| Silico... | GV256              | 256 GB | 2       | 74    | 0     | 0.20   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 2       | 74    | 0     | 0.20   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 2       | 74    | 0     | 0.20   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 5       | 74    | 0     | 0.20   |
| China     | 256GB SSD          | 256 GB | 7       | 74    | 0     | 0.20   |
| Intenso   | Premium            | 250 GB | 2       | 72    | 0     | 0.20   |
| Crucial   | CT1000P3SSD8       | 1 TB   | 8       | 72    | 0     | 0.20   |
| Samsung   | MZVLB256HBHQ-000L7 |        | 15      | 72    | 0     | 0.20   |
| SK hynix  | HFM512GD3JX013N    | 512 GB | 2       | 72    | 0     | 0.20   |
| Fanxiang  | S501               | 128 GB | 19      | 71    | 0     | 0.19   |
| Micron    | 2210_MTFDHBA512QFD | 512 GB | 2       | 71    | 0     | 0.19   |
| Kingston  | SNVS1000G          | 1 TB   | 2       | 70    | 0     | 0.19   |
| SK hynix  | BC711 HFM256GD3... | 256 GB | 4       | 70    | 0     | 0.19   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 5       | 69    | 0     | 0.19   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 2       | 69    | 0     | 0.19   |
| Samsung   | SSD 980 PRO        | 1 TB   | 37      | 67    | 0     | 0.19   |
| Lenovo    | LENSE30512GMSP3... | 512 GB | 2       | 67    | 0     | 0.18   |
| BIWIN     | SSD                | 1 TB   | 3       | 66    | 0     | 0.18   |
| Samsung   | SSD 980 PRO wit... | 2 TB   | 4       | 64    | 0     | 0.18   |
| KIOXIA    | KBG40ZNV256G       | 256 GB | 2       | 64    | 0     | 0.18   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 2       | 63    | 0     | 0.17   |
| Kingston  | RBUSNS8154P3256GJ1 | 256 GB | 4       | 62    | 0     | 0.17   |
| Transcend | TS2TMTE220S        | 2 TB   | 3       | 62    | 0     | 0.17   |
| SK hynix  | PC300 NVMe         | 512 GB | 2       | 62    | 0     | 0.17   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 8       | 62    | 0     | 0.17   |
| Samsung   | PM981a NVMe        | 512 GB | 2       | 61    | 0     | 0.17   |
| Fanxiang  | S500               | 128 GB | 8       | 60    | 0     | 0.17   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 2       | 58    | 0     | 0.16   |
| Samsung   | PM9A1 NVMe         | 1 TB   | 3       | 58    | 0     | 0.16   |
| Patriot   | M.2 P300           | 128 GB | 20      | 57    | 0     | 0.16   |
| Transcend | TS1TMTE720T        | 1 TB   | 7       | 57    | 0     | 0.16   |
| Micron    | 2450 NVMe          | 256 GB | 2       | 57    | 0     | 0.16   |
| Samsung   | MZVLB256HBHQ-00007 | 256 GB | 3       | 55    | 0     | 0.15   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 3       | 54    | 0     | 0.15   |
| Kingston  | OM8PDP3256B-A01    | 256 GB | 8       | 53    | 0     | 0.15   |
| Intel     | SSDPEKNU010TZ      | 1 TB   | 4       | 52    | 0     | 0.14   |
| KIOXIA... | PLUS G3 SSD        | 1 TB   | 2       | 51    | 0     | 0.14   |
| Patriot   | M.2 P300           | 256 GB | 13      | 51    | 0     | 0.14   |
| KIOXIA    | KBG50ZNV256G       | 256 GB | 2       | 50    | 0     | 0.14   |
| China     | NVME SSD           | 128 GB | 11      | 50    | 0     | 0.14   |
| Intel     | SSDPEKNU512GZ      | 512 GB | 12      | 50    | 0     | 0.14   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 3       | 50    | 0     | 0.14   |
| Silico... | GV-128-2242        | 128 GB | 2       | 49    | 0     | 0.14   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 7       | 49    | 0     | 0.14   |
| SanDisk   | WD Blue SN580      | 500 GB | 2       | 47    | 0     | 0.13   |
| Star D... | PCIe SSD           | 960 GB | 3       | 47    | 0     | 0.13   |
| SanDisk   | WD_BLACK SN770     | 1 TB   | 15      | 47    | 0     | 0.13   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 4       | 47    | 0     | 0.13   |
| Union ... | UMIS LENSE40256... | 256 GB | 2       | 47    | 0     | 0.13   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 2       | 47    | 0     | 0.13   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 4       | 46    | 0     | 0.13   |
| SanDisk   | WD Red SN700       | 500 GB | 6       | 46    | 0     | 0.13   |
| Crucial   | CT500P3SSD8        | 500 GB | 30      | 45    | 0     | 0.13   |
| ADATA     | LEGEND 710         | 256 GB | 3       | 45    | 0     | 0.12   |
| SanDisk   | WD_BLACK SN850X    | 2 TB   | 2       | 44    | 0     | 0.12   |
| Intel     | SSDPEK1A118GA      | 118 GB | 11      | 44    | 0     | 0.12   |
| Micron    | 2400_MTFDKBA512QFM | 512 GB | 3       | 43    | 0     | 0.12   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 5       | 43    | 0     | 0.12   |
| Micron    | 2200S NVMe         | 512 GB | 3       | 43    | 0     | 0.12   |
| SanDisk   | WD PC SN740 SDD... |        | 2       | 40    | 0     | 0.11   |
| Samsung   | MZVL2512HCJQ-00BL7 | 512 GB | 2       | 40    | 0     | 0.11   |
| WDC       | WDS480G2G0C-00AJM0 | 480 GB | 2       | 39    | 0     | 0.11   |
| Silico... | BKKJ PCIE 512G     | 512 GB | 2       | 39    | 0     | 0.11   |
| Transcend | TS512GMTE710T      | 512 GB | 3       | 39    | 0     | 0.11   |
| SanDisk   | WD Blue SN570      | 1 TB   | 11      | 38    | 0     | 0.11   |
| Colorful  | CN600              | 512 GB | 2       | 38    | 0     | 0.10   |
| Micron    | MTFDHBA512QFD-1... | 512 GB | 2       | 37    | 0     | 0.10   |
| Kingston  | SNV2S1000G         | 1 TB   | 10      | 37    | 0     | 0.10   |
| BIWIN     | NA80Y1M10-256G     | 256 GB | 3       | 35    | 0     | 0.10   |
| HP        | SSD EX900          | 500 GB | 3       | 35    | 0     | 0.10   |
| SanDisk   | WD Blue SN570 5... | 500 GB | 2       | 34    | 0     | 0.10   |
| Kingston  | OM8PDP3256B-AA1    | 256 GB | 3       | 34    | 0     | 0.09   |
| KIOXIA    | KBG50ZNV512G       | 512 GB | 4       | 34    | 0     | 0.09   |
| Kingston  | SKC3000S1024G      | 1 TB   | 5       | 34    | 0     | 0.09   |
| Samsung   | MZVL41T0HBLB-00BH1 | 1 TB   | 2       | 33    | 0     | 0.09   |
| SanDisk   | WD_BLACK SN770     | 2 TB   | 4       | 33    | 0     | 0.09   |
| Lite-On   | CA3-8D512          | 512 GB | 2       | 33    | 0     | 0.09   |
| Kingston  | OM8PDP3256B-AI1    | 256 GB | 5       | 32    | 0     | 0.09   |
| Kingston  | OM3PGP4128P-AH     | 128 GB | 2       | 32    | 0     | 0.09   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 7       | 32    | 0     | 0.09   |
| Silico... | BKKJ nvme 128G     | 128 GB | 5       | 32    | 0     | 0.09   |
| Silico... | BKKJ pcie 256G     | 256 GB | 2       | 31    | 0     | 0.09   |
| YMTC      | YMSS1ED04B21MC     | 256 GB | 5       | 31    | 0     | 0.09   |
| Kingston  | OM8PCP3512F-AA     | 512 GB | 4       | 31    | 0     | 0.09   |
| ADATA     | SX6000PNP          | 512 GB | 2       | 29    | 0     | 0.08   |
| Gigaby... | GP-GSM2NE3256GNTD  | 256 GB | 3       | 29    | 0     | 0.08   |
| ADATA     | SWORDFISH          | 250 GB | 2       | 28    | 0     | 0.08   |
| Phison    | minisforum         | 512 GB | 2       | 28    | 0     | 0.08   |
| Phison    | YSO128GTLCW-E3C-2  | 128 GB | 7       | 28    | 0     | 0.08   |
| Intenso   | SSD                | 250 GB | 5       | 27    | 0     | 0.08   |
| Samsung   | MZALQ256HAJD-000L1 | 256 GB | 4       | 27    | 0     | 0.07   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 2       | 27    | 0     | 0.07   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 5       | 26    | 0     | 0.07   |
| Crucial   | CT1000P3PSSD8      | 1 TB   | 8       | 26    | 0     | 0.07   |
| SK hynix  | BC711 NVMe         | 256 GB | 5       | 25    | 0     | 0.07   |
| Lexar     | SSD NM620          | 1 TB   | 4       | 24    | 0     | 0.07   |
| Gigaby... | GP-GSM2NE3100TNTD  | 1 TB   | 2       | 22    | 0     | 0.06   |
| SanDisk   | WD Green SN350     | 2 TB   | 2       | 22    | 0     | 0.06   |
| Kingston  | SNV2S500G          | 500 GB | 21      | 25    | 13    | 0.06   |
| Samsung   | MZVL2512HCJQ-00B00 | 512 GB | 3       | 22    | 0     | 0.06   |
| Samsung   | MZALQ128HBHQ-000L2 | 128 GB | 3       | 21    | 0     | 0.06   |
| Mushkin   | MKNSSDHL1TB-D8     | 1 TB   | 2       | 21    | 0     | 0.06   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 2       | 20    | 0     | 0.06   |
| Samsung   | MZVLQ128HCHQ-00BH1 | 128 GB | 7       | 20    | 0     | 0.06   |
| FORESEE   | P900F128GH         | 128 GB | 2       | 20    | 0     | 0.06   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 2       | 19    | 0     | 0.05   |
| Silico... | 512GB SSD          | 512 GB | 2       | 19    | 0     | 0.05   |
| Micron    | 7450_MTFDKBA800TFS |        | 2       | 19    | 0     | 0.05   |
| Crucial   | CT2000P5PSSD8      | 2 TB   | 2       | 18    | 0     | 0.05   |
| SK hynix  | SOLIDIGM SSDPFK... | 2 TB   | 2       | 18    | 0     | 0.05   |
| CWdisk    | 1TB                | 1 TB   | 3       | 17    | 0     | 0.05   |
| Intel     | SSDPEKNU020TZ      | 2 TB   | 2       | 17    | 0     | 0.05   |
| Micron    | 2450_MTFDKBA1T0TFK | 1 TB   | 2       | 17    | 0     | 0.05   |
| GOFATOO   | 512GB SSD          | 512 GB | 4       | 17    | 0     | 0.05   |
| Phison    | YSO256GTLCW-E3C-2  | 256 GB | 5       | 16    | 0     | 0.05   |
| Transcend | TS256GMTE712A      | 256 GB | 5       | 16    | 0     | 0.04   |
| FORESEE   | XP1000F001T        | 1 TB   | 4       | 15    | 0     | 0.04   |
| Phison    | 311CD0128GB        | 128 GB | 2       | 15    | 0     | 0.04   |
| Kingston  | OM8PGP41024Q-A0    | 1 TB   | 4       | 15    | 0     | 0.04   |
| ShiJi     | 128GB M.2-NVMe     | 128 GB | 11      | 14    | 0     | 0.04   |
| SK hynix  | BC511 NVMe         | 512 GB | 4       | 14    | 0     | 0.04   |
| Samsung   | MZVL2512HCJQ-00B07 | 512 GB | 4       | 14    | 0     | 0.04   |
| Faspeed   | P8-512G            | 512 GB | 3       | 13    | 0     | 0.04   |
| BIWIN     | NA80Y1M10-512G     | 512 GB | 7       | 12    | 0     | 0.03   |
| Lexar     | SSD NM620          | 512 GB | 2       | 12    | 0     | 0.03   |
| UMIS      | RPJTJ128MED1MWX    | 128 GB | 3       | 12    | 0     | 0.03   |
| FORESEE   | XP1000F128G        | 128 GB | 3       | 12    | 0     | 0.03   |
| AGI       | AGI512G16AI198     | 512 GB | 2       | 33    | 1     | 0.03   |
| Samsung   | SSD 980 PRO        | 2 TB   | 8       | 119   | 126   | 0.03   |
| ADATA     | SX6000LNP          | 512 GB | 3       | 11    | 0     | 0.03   |
| Kingston  | OM8SEP4512N-A0     | 512 GB | 2       | 11    | 0     | 0.03   |
| Crucial   | CT4000P3SSD8       | 4 TB   | 6       | 10    | 0     | 0.03   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 2       | 10    | 0     | 0.03   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 2       | 9     | 0     | 0.03   |
| Kingston  | SFYRS1000G         | 1 TB   | 3       | 9     | 0     | 0.03   |
| AMD       | R5MP128G8          | 128 GB | 2       | 9     | 0     | 0.03   |
| Samsung   | MZALQ256HAJD-000L2 | 256 GB | 3       | 9     | 0     | 0.03   |
| ADATA     | SX6000PNP          | 256 GB | 3       | 9     | 0     | 0.02   |
| Mushkin   | MKNSSDHL500GB-D8   | 500 GB | 2       | 8     | 0     | 0.02   |
| Samsung   | MZVL2512HCJQ-00BL2 | 512 GB | 2       | 8     | 0     | 0.02   |
| SanDisk   | WD_BLACK SN850     | 1 TB   | 2       | 7     | 0     | 0.02   |
| Samsung   | MZVLQ1T0HBLB-00B00 | 1 TB   | 2       | 7     | 0     | 0.02   |
| WDC       | PC SN530 NVMe      | 256 GB | 3       | 7     | 0     | 0.02   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 3       | 6     | 0     | 0.02   |
| Phison    | Sabrent SB-1342... | 512 GB | 2       | 6     | 0     | 0.02   |
| Kingston  | SFYRD4000G         | 4 TB   | 2       | 6     | 0     | 0.02   |
| Lexar     | SSD NM790          | 1 TB   | 2       | 6     | 0     | 0.02   |
| SanDisk   | WD_BLACK SN850X    | 1 TB   | 2       | 6     | 0     | 0.02   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 2       | 6     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 2       | 5     | 0     | 0.02   |
| CWdisk    | 128G               | 128 GB | 2       | 5     | 0     | 0.02   |
| Intel     | SSDPE2KX010T8      | 1 TB   | 2       | 5     | 0     | 0.02   |
| Lexar     | SSD ARES           | 4 TB   | 2       | 5     | 0     | 0.01   |
| Netac     | NVMe SSD           | 250 GB | 2       | 4     | 0     | 0.01   |
| Faspeed   | P8-256G PLUS       | 256 GB | 3       | 4     | 0     | 0.01   |
| Samsung   | MZALQ512HBLU-00BL1 | 512 GB | 4       | 3     | 0     | 0.01   |
| Silico... | NS256GSSD530       | 256 GB | 3       | 3     | 0     | 0.01   |
| SSSTC     | CL4-8D512          | 512 GB | 4       | 3     | 0     | 0.01   |
| Phison    | ESO512GYLCT-EP3-2L | 512 GB | 2       | 3     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 2       | 3     | 0     | 0.01   |
| Samsung   | MZVL21T0HCLR-00BL7 | 1 TB   | 3       | 3     | 0     | 0.01   |
| BR        | 256GB              | 256 GB | 2       | 3     | 0     | 0.01   |
| FORESEE   | XP1000F512G        | 512 GB | 3       | 2     | 0     | 0.01   |
| Kingston  | OM8PGP4512Q-A0     | 512 GB | 2       | 2     | 0     | 0.01   |
| UMIS      | RPJTJ128MEE1MWX    | 128 GB | 2       | 2     | 0     | 0.01   |
| Samsung   | MZVL4256HBJD-00BH1 | 256 GB | 2       | 2     | 0     | 0.01   |
| Silico... | BKKJ nvme 256G     | 256 GB | 3       | 1     | 0     | 0.01   |
| Faspeed   | P8-128G            |        | 4       | 1     | 0     | 0.01   |
| Silico... | 256GB              | 256 GB | 2       | 1     | 0     | 0.00   |
| Kingston  | OM8SEP4512Q-A0     | 512 GB | 4       | 1     | 0     | 0.00   |
| SanDisk   | WD PC SN740 SDD... | 256 GB | 2       | 1     | 0     | 0.00   |
| BR        | 128GB              | 128 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | SSD 990 PRO        | 1 TB   | 6       | 0     | 0     | 0.00   |
| ShiJi     | 256GB M.2-NVMe     | 256 GB | 3       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 3       | 0     | 0     | 0.00   |
| KINGBANK  | KP230              | 120 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | MZ1L2960HCJR-00A07 |        | 2       | 0     | 0     | 0.00   |

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
| Toshiba     | 17     | 60      | 426   | 0     | 1.17   |
| Plextor     | 1      | 3       | 390   | 69    | 0.93   |
| Dell        | 1      | 2       | 336   | 0     | 0.92   |
| Timetec     | 1      | 2       | 335   | 0     | 0.92   |
| Intel       | 32     | 164     | 314   | 1     | 0.83   |
| XPG         | 1      | 7       | 274   | 0     | 0.75   |
| Corsair     | 6      | 17      | 272   | 0     | 0.75   |
| KIOXIA-E... | 3      | 9       | 261   | 0     | 0.72   |
| WDC         | 47     | 227     | 258   | 0     | 0.71   |
| Seagate     | 2      | 9       | 257   | 0     | 0.71   |
| minisforum  | 1      | 2       | 246   | 0     | 0.68   |
| ADATA       | 10     | 45      | 256   | 2     | 0.67   |
| PNY         | 3      | 9       | 234   | 0     | 0.64   |
| HP          | 6      | 27      | 234   | 0     | 0.64   |
| Acer        | 1      | 3       | 222   | 0     | 0.61   |
| Phison      | 13     | 94      | 217   | 0     | 0.60   |
| Samsung     | 97     | 887     | 212   | 2     | 0.56   |
| HGST        | 1      | 2       | 199   | 0     | 0.55   |
| Transcend   | 9      | 97      | 165   | 0     | 0.45   |
| SSSTC       | 3      | 10      | 165   | 0     | 0.45   |
| Goodram     | 1      | 3       | 160   | 0     | 0.44   |
| EDILOCA     | 1      | 2       | 156   | 0     | 0.43   |
| Gigabyte    | 2      | 16      | 155   | 0     | 0.43   |
| Lexar       | 7      | 24      | 153   | 0     | 0.42   |
| Lenovo      | 2      | 4       | 152   | 0     | 0.42   |
| SK hynix    | 25     | 86      | 151   | 1     | 0.41   |
| Team        | 5      | 30      | 144   | 0     | 0.40   |
| Kimtigo     | 1      | 8       | 144   | 0     | 0.40   |
| SPCC        | 6      | 42      | 149   | 25    | 0.39   |
| LDLC        | 1      | 2       | 134   | 0     | 0.37   |
| KIOXIA      | 10     | 39      | 131   | 0     | 0.36   |
| Gigabyte... | 3      | 7       | 129   | 0     | 0.35   |
| ORTIAL      | 1      | 2       | 122   | 0     | 0.34   |
| Kingston    | 34     | 188     | 120   | 7     | 0.33   |
| Micron      | 18     | 44      | 125   | 2     | 0.33   |
| Crucial     | 18     | 169     | 117   | 2     | 0.32   |
| ATP         | 1      | 8       | 115   | 0     | 0.32   |
| Silicon ... | 15     | 51      | 96    | 0     | 0.27   |
| Fanxiang    | 5      | 42      | 96    | 0     | 0.26   |
| Netac       | 3      | 7       | 84    | 0     | 0.23   |
| SanDisk     | 18     | 112     | 74    | 0     | 0.20   |
| China       | 3      | 62      | 73    | 1     | 0.20   |
| Patriot     | 4      | 40      | 66    | 0     | 0.18   |
| UMIS        | 3      | 7       | 48    | 0     | 0.13   |
| Star Drive  | 1      | 3       | 47    | 0     | 0.13   |
| Union Me... | 1      | 2       | 47    | 0     | 0.13   |
| Intenso     | 2      | 7       | 40    | 0     | 0.11   |
| FORESEE     | 5      | 14      | 40    | 0     | 0.11   |
| Colorful    | 1      | 2       | 38    | 0     | 0.10   |
| Lite-On     | 1      | 2       | 33    | 0     | 0.09   |
| YMTC        | 1      | 5       | 31    | 0     | 0.09   |
| BIWIN       | 3      | 13      | 30    | 0     | 0.08   |
| GOFATOO     | 1      | 4       | 17    | 0     | 0.05   |
| Mushkin     | 2      | 4       | 15    | 0     | 0.04   |
| CWdisk      | 2      | 5       | 12    | 0     | 0.04   |
| AGI         | 1      | 2       | 33    | 1     | 0.03   |
| ShiJi       | 2      | 14      | 11    | 0     | 0.03   |
| AMD         | 1      | 2       | 9     | 0     | 0.03   |
| Faspeed     | 3      | 10      | 6     | 0     | 0.02   |
| BR          | 2      | 4       | 2     | 0     | 0.01   |
| KINGBANK    | 1      | 2       | 0     | 0     | 0.00   |

