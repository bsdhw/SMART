HDD/SSD Reliability Test
========================

This is a project to estimate reliability of HDD/SSD drives by
the analysis of SMART data collected by BSD users at https://bsd-hardware.info. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe/blob/master/INSTALL.BSD.md) tool:

    hw-probe -all -upload

Total drives: 12424.

Contents
--------

1. [ About          ](#about)
2. [ HDD by Model   ](#hdd-by-model)
3. [ HDD by Family  ](#hdd-by-family)
4. [ HDD by Vendor  ](#hdd-by-vendor)
5. [ SSD by Model   ](#ssd-by-model)
6. [ SSD by Family  ](#ssd-by-family)
7. [ SSD by Vendor  ](#ssd-by-vendor)
8. [ NVMe by Model  ](#nvme-by-model)
9. [ NVMe by Vendor ](#nvme-by-vendor)

About
-----

The structure of the reports directory is the following:

    {KIND OF DRIVE}/{VENDOR}/{MODEL PREFIX}/{MODEL}/{DRIVE ID}

    ( e.g. HDD/Seagate/ST1000/ST1000LM035-1RK172/3F1554E2F97E )

Based on SMART data we determine most reliable drive models and vendors by the
following formula:

    MTBF = MAX( Power_On_Hours / ( 1 + Number_Of_Important_Errors ) ) / ( 365*24 )

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

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| WDC       | WD800JD-08MSA1     | 80 GB  | 1       | 5298  | 0     | 14.52  |
| Seagate   | ST3120023A         | 120 GB | 1       | 5214  | 0     | 14.29  |
| WDC       | WD1600JS-70SGB1    | 160 GB | 1       | 4256  | 0     | 11.66  |
| WDC       | WD1600AAJS-00PSA0  | 160 GB | 1       | 4208  | 0     | 11.53  |
| WDC       | WD1600JB-00REA0    | 160 GB | 1       | 4140  | 0     | 11.34  |
| WDC       | WD1600JD-00GBB0    | 160 GB | 4       | 5313  | 4     | 11.14  |
| WDC       | WD1602ABJS-43P5A0  | 160 GB | 1       | 4045  | 0     | 11.08  |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 3       | 3833  | 0     | 10.50  |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 1       | 3820  | 0     | 10.47  |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 2       | 3820  | 0     | 10.47  |
| WDC       | WD2500AAJS-00V4A0  | 250 GB | 1       | 3798  | 0     | 10.41  |
| Samsung   | HE160HJ            | 160 GB | 1       | 3740  | 0     | 10.25  |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 3       | 3586  | 0     | 9.83   |
| Hitachi   | HDT721032SLA360    | 320 GB | 1       | 3534  | 0     | 9.68   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 4       | 3474  | 0     | 9.52   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 1       | 3468  | 0     | 9.50   |
| WDC       | WD1600BEKT-75A25T0 | 160 GB | 1       | 3424  | 0     | 9.38   |
| Hitachi   | HDS725050KLA360    | 500 GB | 4       | 3376  | 0     | 9.25   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 1       | 3370  | 0     | 9.23   |
| WDC       | WD1600AAJS-60M0A1  | 160 GB | 1       | 3365  | 0     | 9.22   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 2       | 3285  | 0     | 9.00   |
| Seagate   | ST3300831AS        | 304 GB | 1       | 3187  | 0     | 8.73   |
| WDC       | WD7500AAVS-00M4B0  | 752 GB | 1       | 3149  | 0     | 8.63   |
| Seagate   | ST3360320AS        | 360 GB | 1       | 3125  | 0     | 8.56   |
| Seagate   | ST320011A          | 20 GB  | 1       | 3104  | 0     | 8.50   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 3       | 3099  | 0     | 8.49   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 6       | 3085  | 0     | 8.45   |
| Toshiba   | MK2565GSX          | 250 GB | 1       | 3055  | 0     | 8.37   |
| WDC       | WD5000LUCT-63Y8HY0 | 500 GB | 1       | 3053  | 0     | 8.36   |
| WDC       | WD1602ABKS-18N8A0  | 160 GB | 1       | 2978  | 0     | 8.16   |
| WDC       | WD800EB-00DJF0     | 80 GB  | 1       | 2959  | 0     | 8.11   |
| Seagate   | ST3808110AS        | 80 GB  | 2       | 2844  | 0     | 7.79   |
| WDC       | WD400BB-00JHC0     | 40 GB  | 1       | 2834  | 0     | 7.77   |
| Seagate   | ST500DL001 HD503HI | 500 GB | 1       | 2831  | 0     | 7.76   |
| Seagate   | ST3500630NS        | 500 GB | 5       | 2821  | 0     | 7.73   |
| WDC       | WD400BB-00GFA0     | 40 GB  | 1       | 2808  | 0     | 7.69   |
| Hitachi   | HUA7250SBSUN500G   | 500 GB | 2       | 2785  | 0     | 7.63   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 1       | 2772  | 0     | 7.59   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 1       | 2760  | 0     | 7.56   |
| HGST      | HUS724030ALA640    | 3 TB   | 1       | 2737  | 0     | 7.50   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 4       | 2729  | 0     | 7.48   |
| WDC       | WD3000HLHX-60JJPV0 | 304 GB | 1       | 2710  | 0     | 7.43   |
| WDC       | WD3200AAKX-00ERMA0 | 320 GB | 1       | 2660  | 0     | 7.29   |
| MARVELL   | Raid VD            | 249 GB | 1       | 2636  | 0     | 7.22   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 2       | 2628  | 0     | 7.20   |
| Seagate   | ST33000651NS       | 3 TB   | 1       | 2619  | 0     | 7.18   |
| Hitachi   | HDT725025VLA380    | 250 GB | 2       | 2611  | 0     | 7.15   |
| Seagate   | ST3320413AS        | 320 GB | 2       | 2575  | 0     | 7.06   |
| Hitachi   | HUA721050KLA330    | 500 GB | 2       | 3842  | 1     | 7.02   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 3       | 2560  | 0     | 7.01   |
| Samsung   | HD502IJ            | 500 GB | 2       | 2696  | 1     | 6.93   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 1       | 2510  | 0     | 6.88   |
| WDC       | WD10EACS-65D6B0    | 1 TB   | 1       | 2509  | 0     | 6.88   |
| Seagate   | ST32000641AS       | 2 TB   | 5       | 2443  | 0     | 6.69   |
| WDC       | WD2500JD-75HBB0    | 250 GB | 1       | 2439  | 0     | 6.68   |
| WDC       | WD1600AABS-61PRA0  | 160 GB | 1       | 2420  | 0     | 6.63   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 1       | 2414  | 0     | 6.61   |
| Seagate   | ST2000VX002-1AH166 | 2 TB   | 1       | 2412  | 0     | 6.61   |
| HP        | GB0250EAFYK        | 250 GB | 3       | 3054  | 1     | 6.61   |
| WDC       | WD1600AAJS-00Z4A0  | 160 GB | 2       | 2386  | 0     | 6.54   |
| Hitachi   | HDS5C1010CLA382    | 1 TB   | 1       | 2374  | 0     | 6.51   |
| Maxtor    | 6V080E0            | 82 GB  | 1       | 2371  | 0     | 6.50   |
| Seagate   | MM0500GBKAK        | 500 GB | 1       | 2355  | 0     | 6.45   |
| Seagate   | ST380011A          | 80 GB  | 2       | 2353  | 0     | 6.45   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 2       | 2343  | 0     | 6.42   |
| Seagate   | ST500LX003-1AC15G  | 500 GB | 1       | 2334  | 0     | 6.40   |
| WDC       | WD30EURX-63T0FY0   | 3 TB   | 1       | 2331  | 0     | 6.39   |
| HGST      | HUS724020ALA640    | 2 TB   | 10      | 2329  | 0     | 6.38   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 3       | 2324  | 0     | 6.37   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 9       | 2520  | 1     | 6.36   |
| WDC       | WD1003FBYX-23 0... | 1 TB   | 2       | 2317  | 0     | 6.35   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 2       | 2315  | 0     | 6.35   |
| WDC       | WD5002ABYS-18B1B0  | 500 GB | 3       | 2880  | 3     | 6.33   |
| WDC       | WD1000FYPS-01ZKB0  | 1 TB   | 1       | 2306  | 0     | 6.32   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 1       | 2298  | 0     | 6.30   |
| Hitachi   | HDT725032VLA360    | 320 GB | 2       | 3927  | 2     | 6.26   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 9       | 2273  | 0     | 6.23   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 1       | 2257  | 0     | 6.19   |
| Seagate   | ST2000VM003-1CT164 | 2 TB   | 1       | 2226  | 0     | 6.10   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 1       | 2187  | 0     | 5.99   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 2168  | 0     | 5.94   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 6       | 2365  | 1     | 5.84   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 27      | 2494  | 1     | 5.84   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 1       | 2120  | 0     | 5.81   |
| HP        | GB0500EAFYL        | 500 GB | 4       | 2079  | 0     | 5.70   |
| Hitachi   | HDS5C4040ALE630    | 4 TB   | 21      | 2076  | 0     | 5.69   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 2       | 2075  | 0     | 5.69   |
| WDC       | WD3200BEKT-08PVMT1 | 320 GB | 5       | 2075  | 0     | 5.69   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 1       | 2072  | 0     | 5.68   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 4       | 2069  | 0     | 5.67   |
| Seagate   | ST250DM000-1BC141  | 250 GB | 1       | 2052  | 0     | 5.62   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 2       | 2045  | 0     | 5.60   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 6       | 3011  | 2     | 5.57   |
| Hitachi   | HDS728080PLA380    | 82 GB  | 2       | 2026  | 0     | 5.55   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 2       | 2009  | 0     | 5.51   |
| WDC       | WD5000AAJS-00A8B2  | 500 GB | 1       | 2008  | 0     | 5.50   |
| WDC       | WD3000BLFS-01YBU0  | 304 GB | 1       | 2006  | 0     | 5.50   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 2       | 2004  | 0     | 5.49   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 7       | 1993  | 0     | 5.46   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 1       | 1983  | 0     | 5.43   |
| Seagate   | ST3400633AS        | 400 GB | 1       | 1978  | 0     | 5.42   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 6       | 1976  | 0     | 5.42   |
| Hitachi   | HTE543232A7A384    | 320 GB | 3       | 1975  | 0     | 5.41   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 12      | 2549  | 64    | 5.39   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 7       | 2118  | 145   | 5.32   |
| Seagate   | ST32000645NS       | 2 TB   | 2       | 1938  | 0     | 5.31   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 1       | 1925  | 0     | 5.28   |
| WDC       | WD2000JD-00FYB0    | 200 GB | 1       | 3833  | 1     | 5.25   |
| Seagate   | ST3320620A         | 320 GB | 1       | 1913  | 0     | 5.24   |
| WDC       | WD360ADFD-00NLR5   | 37 GB  | 1       | 1910  | 0     | 5.23   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 18      | 2020  | 2     | 5.23   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 6       | 2191  | 2     | 5.20   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 1       | 1894  | 0     | 5.19   |
| Hitachi   | HDT721032SLA380    | 320 GB | 1       | 1893  | 0     | 5.19   |
| Seagate   | ST3160215ACE       | 160 GB | 1       | 1863  | 0     | 5.11   |
| HGST      | HTE721010A9E630    | 1 TB   | 3       | 1849  | 0     | 5.07   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 1       | 1848  | 0     | 5.06   |
| Hitachi   | HCC543216A7A380    | 160 GB | 1       | 1843  | 0     | 5.05   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 10      | 1993  | 2     | 5.01   |
| WDC       | WD2500AAKX-753CA1  | 250 GB | 3       | 1828  | 0     | 5.01   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 1       | 1824  | 0     | 5.00   |
| HGST      | HUH728060ALE600    | 6 TB   | 1       | 1820  | 0     | 4.99   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 1       | 1819  | 0     | 4.98   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 2       | 1816  | 0     | 4.98   |
| Seagate   | ST1500DL003-9VT16L | 1.5 TB | 1       | 1816  | 0     | 4.98   |
| Seagate   | ST4000NC000-1FR168 | 4 TB   | 2       | 1810  | 0     | 4.96   |
| Hitachi   | HTE545050B9A300    | 500 GB | 1       | 1809  | 0     | 4.96   |
| Maxtor    | STM3250820A        | 250 GB | 1       | 1802  | 0     | 4.94   |
| Seagate   | ST9320421AS        | 320 GB | 1       | 1802  | 0     | 4.94   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 14      | 1892  | 145   | 4.92   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 3       | 1792  | 0     | 4.91   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 2       | 3527  | 3     | 4.88   |
| Toshiba   | MG03ACA200         | 2 TB   | 6       | 1760  | 0     | 4.82   |
| HGST      | HDN724040ALE640    | 4 TB   | 17      | 2042  | 48    | 4.81   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 4       | 1752  | 0     | 4.80   |
| HGST      | HDN724030ALE640    | 3 TB   | 7       | 1737  | 0     | 4.76   |
| WDC       | WD60PURZ-85ZUFY1   | 6 TB   | 1       | 1735  | 0     | 4.76   |
| WDC       | WD3200BEKT-75KA9T0 | 320 GB | 1       | 1730  | 0     | 4.74   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 15      | 1963  | 83    | 4.74   |
| WDC       | WD6002FZWX-00GBGB0 | 6 TB   | 1       | 1727  | 0     | 4.73   |
| Hitachi   | HTS725050A9A362    | 500 GB | 1       | 1722  | 0     | 4.72   |
| Seagate   | ST6000DX000-1H217Z | 6 TB   | 2       | 1714  | 0     | 4.70   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 1       | 1699  | 0     | 4.66   |
| Seagate   | ST3500412AS        | 500 GB | 1       | 1696  | 0     | 4.65   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 15      | 1951  | 135   | 4.64   |
| Seagate   | ST1000LM014-1EJ... | 1 TB   | 1       | 1670  | 0     | 4.58   |
| WDC       | WD30NMRW-11YL9S4   | 3 TB   | 1       | 1667  | 0     | 4.57   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 33      | 1719  | 32    | 4.56   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 4       | 2240  | 2     | 4.52   |
| WDC       | WD5000BEVT-00A03T0 | 500 GB | 1       | 1643  | 0     | 4.50   |
| Seagate   | ST3500414CS        | 500 GB | 6       | 1643  | 6     | 4.50   |
| Toshiba   | MG04ACA400E        | 4 TB   | 2       | 1635  | 0     | 4.48   |
| Toshiba   | MK3276GSX -63      | 320 GB | 1       | 1634  | 0     | 4.48   |
| HGST      | HTS725050A7E635... | 500 GB | 1       | 1625  | 0     | 4.45   |
| Hitachi   | HTS725032A9A360    | 320 GB | 1       | 1622  | 0     | 4.45   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 2       | 1617  | 0     | 4.43   |
| Seagate   | ST8000DM002-1YW112 | 8 TB   | 1       | 1614  | 0     | 4.42   |
| Hitachi   | HUA721075KLA330    | 752 GB | 2       | 1592  | 0     | 4.36   |
| Hitachi   | HDS721050DLE630    | 500 GB | 1       | 1580  | 0     | 4.33   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 4       | 1574  | 0     | 4.31   |
| Samsung   | HD103SJ            | 1 TB   | 7       | 2056  | 1     | 4.31   |
| Samsung   | HD204UI            | 2 TB   | 20      | 2071  | 7     | 4.30   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 8       | 1557  | 0     | 4.27   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 3       | 3550  | 4     | 4.25   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 3       | 1544  | 0     | 4.23   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 1       | 1543  | 0     | 4.23   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 2       | 2555  | 545   | 4.22   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 1       | 1531  | 0     | 4.20   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 5       | 1520  | 0     | 4.17   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 2       | 1517  | 0     | 4.16   |
| Maxtor    | 6L080J4            | 80 GB  | 3       | 2093  | 2     | 4.15   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 2       | 1504  | 0     | 4.12   |
| WDC       | WD7500BMVW-11AJGS4 | 752 GB | 1       | 1500  | 0     | 4.11   |
| HP        | MB1000GCWCV        | 1 TB   | 7       | 2004  | 4     | 4.09   |
| WDC       | WD5000LUCT-63RC2Y0 | 500 GB | 1       | 1477  | 0     | 4.05   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 4       | 1560  | 1     | 4.05   |
| WDC       | WD2500JS-75NCB2    | 250 GB | 4       | 1473  | 0     | 4.04   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 9       | 2227  | 229   | 4.03   |
| WDC       | WD2000FYYX         | 2 TB   | 4       | 1466  | 0     | 4.02   |
| WDC       | WD2500AAJS-07M0A0  | 250 GB | 1       | 1462  | 0     | 4.01   |
| Hitachi   | HDE721064SLA360    | 640 GB | 2       | 2248  | 6     | 4.00   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 4       | 1909  | 1     | 3.97   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 2       | 1450  | 0     | 3.97   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 2       | 1449  | 0     | 3.97   |
| Hitachi   | HDP725050GLA360    | 500 GB | 4       | 1735  | 10    | 3.97   |
| WDC       | WD10PURX-64D85Y0   | 1 TB   | 1       | 1445  | 0     | 3.96   |
| Hitachi   | HDS728080PLAT20    | 82 GB  | 1       | 1438  | 0     | 3.94   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 3       | 1529  | 3     | 3.92   |
| Hitachi   | HDS721050CLA360    | 500 GB | 1       | 1429  | 0     | 3.92   |
| Hitachi   | HDS721075KLA330    | 752 GB | 9       | 1767  | 1     | 3.90   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 1       | 1421  | 0     | 3.89   |
| Toshiba   | MD04ACA500         | 5 TB   | 1       | 1413  | 0     | 3.87   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 4       | 2658  | 3     | 3.85   |
| Samsung   | HD502HI            | 500 GB | 2       | 1402  | 0     | 3.84   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 13      | 1398  | 0     | 3.83   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 2       | 2462  | 14    | 3.82   |
| WDC       | WD2500AAJS-00L7A0  | 250 GB | 1       | 1391  | 0     | 3.81   |
| Seagate   | ST3250312AS        | 250 GB | 6       | 1380  | 0     | 3.78   |
| Seagate   | ST1000NX0313       | 1 TB   | 1       | 1380  | 0     | 3.78   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 14      | 2309  | 158   | 3.78   |
| HP        | VB0250EAVER        | 250 GB | 3       | 2037  | 2     | 3.76   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 3       | 1368  | 0     | 3.75   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 4       | 1366  | 0     | 3.74   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 36      | 1756  | 1     | 3.73   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 5       | 1352  | 0     | 3.71   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 4       | 1797  | 28    | 3.71   |
| Hitachi   | HTS541060G9AT00    | 64 GB  | 1       | 1351  | 0     | 3.70   |
| WDC       | WD2500AAKX-753CA0  | 250 GB | 1       | 2694  | 1     | 3.69   |
| Seagate   | ST6000DM001-1YW11C | 6 TB   | 1       | 1338  | 0     | 3.67   |
| Samsung   | HD322HJ            | 320 GB | 10      | 1524  | 61    | 3.67   |
| WDC       | WD1600BEVS-75RST0  | 160 GB | 1       | 1336  | 0     | 3.66   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 6       | 1333  | 0     | 3.65   |
| Hitachi   | HDT721025SLA380    | 250 GB | 1       | 1332  | 0     | 3.65   |
| WDC       | WD20NMVW-11EDZS2   | 2 TB   | 2       | 1324  | 0     | 3.63   |
| Hitachi   | HDS721032CLA362    | 320 GB | 1       | 1323  | 0     | 3.63   |
| Toshiba   | MG04ACA100N        | 1 TB   | 2       | 1323  | 0     | 3.62   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 1       | 1317  | 0     | 3.61   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 3       | 1317  | 0     | 3.61   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 2       | 1313  | 0     | 3.60   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 69      | 1529  | 1     | 3.60   |
| WDC       | WD5000BMVV-11A1CS0 | 500 GB | 1       | 1308  | 0     | 3.59   |
| WDC       | WD2503ABYZ-011FA0  | 256 GB | 2       | 1306  | 0     | 3.58   |
| Toshiba   | MK2561GSYB         | 250 GB | 2       | 1306  | 0     | 3.58   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 34      | 1723  | 57    | 3.57   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 4       | 1301  | 0     | 3.57   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 7       | 1301  | 0     | 3.57   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 1       | 1296  | 0     | 3.55   |
| Seagate   | ST33000651AS       | 3 TB   | 2       | 1296  | 0     | 3.55   |
| WDC       | WD10EZEX-00ZF5A0   | 1 TB   | 1       | 1294  | 0     | 3.55   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 2       | 1632  | 1     | 3.52   |
| Samsung   | HD154UI            | 1.5 TB | 8       | 2606  | 276   | 3.52   |
| Seagate   | ST9500423AS        | 500 GB | 1       | 1283  | 0     | 3.52   |
| WDC       | WD5003ABYX-88 LEN  | 500 GB | 1       | 1280  | 0     | 3.51   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 2       | 1268  | 0     | 3.48   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 1       | 1266  | 0     | 3.47   |
| Samsung   | HD161GJ            | 160 GB | 3       | 1263  | 0     | 3.46   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 2       | 1260  | 0     | 3.45   |
| Seagate   | ST9500620NS        | 500 GB | 3       | 2190  | 25    | 3.45   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 1       | 1260  | 0     | 3.45   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 3       | 1255  | 0     | 3.44   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 8       | 1244  | 0     | 3.41   |
| WDC       | WD3200BEKT-00A25T0 | 320 GB | 1       | 1239  | 0     | 3.40   |
| HGST      | HUS726040ALN610    | 4 TB   | 2       | 1239  | 0     | 3.40   |
| WDC       | WD1600AAJS-00V4A0  | 160 GB | 1       | 1238  | 0     | 3.39   |
| WDC       | WD5000AAKS-75A7B0  | 500 GB | 1       | 1238  | 0     | 3.39   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 3       | 1236  | 0     | 3.39   |
| WDC       | WD3200AAKX-001CA0  | 320 GB | 3       | 2227  | 5     | 3.38   |
| Toshiba   | DT01ACA200         | 2 TB   | 12      | 1375  | 95    | 3.37   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 13      | 1304  | 1     | 3.35   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 1       | 3656  | 2     | 3.34   |
| WDC       | WD3201ABYS-01B9A0  | 320 GB | 1       | 1214  | 0     | 3.33   |
| HP        | FB160C4081         | 160 GB | 3       | 3197  | 3     | 3.32   |
| Toshiba   | HDWA130            | 3 TB   | 1       | 1207  | 0     | 3.31   |
| WDC       | WD1600BEVT-22A23T0 | 160 GB | 2       | 1205  | 0     | 3.30   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 1       | 3610  | 2     | 3.30   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 8       | 1506  | 2     | 3.30   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 2       | 2395  | 260   | 3.29   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 10      | 1199  | 0     | 3.29   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 3       | 1629  | 24    | 3.25   |
| HGST      | HDN728080ALE604    | 8 TB   | 7       | 1182  | 0     | 3.24   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 4       | 1181  | 0     | 3.24   |
| WDC       | WD3750LMCW-11D9GS3 | 375 GB | 1       | 1179  | 0     | 3.23   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 3       | 1167  | 0     | 3.20   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 6       | 1679  | 2     | 3.20   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 6       | 1273  | 1     | 3.19   |
| WDC       | WD1001FALS-403AA0  | 1 TB   | 3       | 1495  | 264   | 3.19   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 1       | 1158  | 0     | 3.17   |
| Samsung   | SP2504C            | 250 GB | 1       | 1158  | 0     | 3.17   |
| WDC       | WD10EURX-73C57Y0   | 1 TB   | 1       | 1156  | 0     | 3.17   |
| Seagate   | ST1000VX001-1Z4102 | 1 TB   | 1       | 1156  | 0     | 3.17   |
| WDC       | WD800JD-08LSA0     | 80 GB  | 1       | 1155  | 0     | 3.17   |
| WDC       | WD5000AACS-00ZUB0  | 500 GB | 2       | 1155  | 0     | 3.16   |
| WDC       | WD20SMZW-11YFCS0   | 2 TB   | 1       | 1154  | 0     | 3.16   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 1       | 1146  | 0     | 3.14   |
| WDC       | WD3000BLFS-60YBU2  | 304 GB | 2       | 1399  | 1     | 3.13   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 6       | 2271  | 46    | 3.13   |
| WDC       | WD7500BPVX-60JC3T0 | 752 GB | 1       | 1138  | 0     | 3.12   |
| Seagate   | ST3320613AS        | 320 GB | 2       | 1995  | 11    | 3.10   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 2       | 1415  | 4     | 3.09   |
| Hitachi   | HDS5C1050CLA382    | 500 GB | 1       | 1123  | 0     | 3.08   |
| WDC       | WD3200JS-22PDB0    | 320 GB | 1       | 1122  | 0     | 3.08   |
| Seagate   | ST500DM009-2DM14C  | 500 GB | 1       | 1122  | 0     | 3.08   |
| Hitachi   | HTS545016B9A300    | 160 GB | 2       | 1116  | 0     | 3.06   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 2       | 2202  | 3     | 3.05   |
| WDC       | WD2005FBYZ-01YCBB1 | 2 TB   | 2       | 1111  | 0     | 3.05   |
| WDC       | WD3200BEKT-00KA9T0 | 320 GB | 2       | 1109  | 0     | 3.04   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 5       | 1105  | 0     | 3.03   |
| WDC       | WD360GD-00FLC0     | 37 GB  | 1       | 1099  | 0     | 3.01   |
| Samsung   | HD502HJ            | 500 GB | 8       | 1709  | 2     | 3.01   |
| WDC       | WD2000JB-00FUA0    | 200 GB | 1       | 1089  | 0     | 2.98   |
| WDC       | WD5000BEKT-22KA9T0 | 500 GB | 1       | 1085  | 0     | 2.97   |
| Seagate   | ST320VT000-1BS14C  | 320 GB | 1       | 1083  | 0     | 2.97   |
| WDC       | WD4002FYYZ-01B7CB0 | 4 TB   | 3       | 1082  | 0     | 2.97   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 7       | 1081  | 0     | 2.96   |
| WDC       | WD20NMVW-59EDZS7   | 2 TB   | 1       | 1075  | 0     | 2.95   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 28      | 1264  | 132   | 2.94   |
| WDC       | WD10EADX-00TDHB0   | 1 TB   | 1       | 1070  | 0     | 2.93   |
| Toshiba   | MQ01UBB200         | 2 TB   | 1       | 1067  | 0     | 2.93   |
| HGST      | HUS724040ALA640    | 4 TB   | 5       | 1058  | 0     | 2.90   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 1       | 1057  | 0     | 2.90   |
| Seagate   | ST3160023A         | 160 GB | 1       | 1056  | 0     | 2.89   |
| WDC       | WD1200BEVS-07RST0  | 120 GB | 1       | 1053  | 0     | 2.89   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 1       | 1053  | 0     | 2.89   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 3       | 1273  | 1     | 2.88   |
| WDC       | WD3200AAKS-75L9A0  | 320 GB | 2       | 1472  | 2     | 2.86   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 3       | 1073  | 7     | 2.85   |
| Toshiba   | MQ01ABD100H        | 1 TB   | 2       | 1041  | 0     | 2.85   |
| Seagate   | ST3160318AS        | 160 GB | 11      | 1312  | 49    | 2.84   |
| HGST      | HDN726040ALE614    | 4 TB   | 4       | 1032  | 0     | 2.83   |
| Seagate   | ST3500413AS        | 500 GB | 18      | 1379  | 279   | 2.82   |
| Toshiba   | MC04ACA400E        | 4 TB   | 2       | 1023  | 0     | 2.80   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 11      | 1090  | 184   | 2.80   |
| Samsung   | HD321HJ            | 320 GB | 1       | 1021  | 0     | 2.80   |
| Samsung   | HD103UJ            | 1 TB   | 9       | 1787  | 27    | 2.79   |
| ExcelStor | J8160              | 164 GB | 2       | 1015  | 0     | 2.78   |
| WDC       | WD1600AAJS-60Z0A0  | 160 GB | 2       | 1443  | 803   | 2.77   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 3       | 1293  | 3     | 2.76   |
| WDC       | WD2500AAKX-073CA1  | 250 GB | 1       | 1007  | 0     | 2.76   |
| Samsung   | HD251HJ            | 250 GB | 1       | 1007  | 0     | 2.76   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 1       | 1005  | 0     | 2.76   |
| HPE       | MB4000GVYZK        | 4 TB   | 8       | 1005  | 0     | 2.76   |
| Toshiba   | HDWE150            | 5 TB   | 6       | 1186  | 5     | 2.73   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 5       | 2630  | 386   | 2.73   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 1       | 991   | 0     | 2.72   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 2       | 990   | 0     | 2.71   |
| WDC       | WD3200AAKS-75SBA0  | 320 GB | 1       | 990   | 0     | 2.71   |
| Samsung   | HM500JI            | 500 GB | 4       | 1251  | 53    | 2.71   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 2       | 986   | 0     | 2.70   |
| Seagate   | ST3250318AS        | 250 GB | 10      | 1302  | 90    | 2.70   |
| Seagate   | ST9160411AS        | 160 GB | 2       | 1221  | 3     | 2.68   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 4       | 1837  | 326   | 2.68   |
| WDC       | WD1600AAJS-40H3A0  | 160 GB | 2       | 975   | 0     | 2.67   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 3       | 974   | 0     | 2.67   |
| Seagate   | ST3160316CS        | 160 GB | 1       | 972   | 0     | 2.66   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 2       | 972   | 0     | 2.66   |
| Seagate   | ST380815AS         | 80 GB  | 10      | 1504  | 553   | 2.66   |
| Samsung   | HD501LJ            | 500 GB | 11      | 2219  | 280   | 2.65   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 1449  | 1     | 2.65   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 19      | 1085  | 62    | 2.65   |
| Samsung   | HD203WI            | 2 TB   | 1       | 959   | 0     | 2.63   |
| Toshiba   | MQ01ABB200         | 2 TB   | 1       | 953   | 0     | 2.61   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 4       | 950   | 0     | 2.60   |
| Seagate   | ST32000542AS       | 2 TB   | 3       | 1273  | 321   | 2.60   |
| Seagate   | ST3000DM003-2AE16L | 3 TB   | 1       | 947   | 0     | 2.60   |
| Fujitsu   | MHW2120BH          | 120 GB | 2       | 945   | 0     | 2.59   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 19      | 945   | 0     | 2.59   |
| Seagate   | ST3750528AS        | 752 GB | 3       | 1686  | 45    | 2.57   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 4       | 1234  | 2     | 2.57   |
| Toshiba   | DT01ACA300         | 3 TB   | 15      | 1101  | 69    | 2.57   |
| WDC       | WD3200BEVS-08VAT2  | 320 GB | 1       | 936   | 0     | 2.57   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 22      | 1000  | 1     | 2.56   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 3       | 1428  | 5     | 2.56   |
| Seagate   | ST3250820AS Q      | 250 GB | 1       | 932   | 0     | 2.55   |
| WDC       | WD20SDZW-11JJ8S0   | 2 TB   | 1       | 929   | 0     | 2.55   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 14      | 1205  | 35    | 2.55   |
| CLOVER    | CD253GJ            | 250 GB | 1       | 928   | 0     | 2.54   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 11      | 925   | 0     | 2.54   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 10      | 1459  | 233   | 2.53   |
| HGST      | HDN721010ALE604    | 10 TB  | 3       | 916   | 0     | 2.51   |
| Seagate   | ST3500312CS        | 500 GB | 15      | 1032  | 64    | 2.50   |
| WDC       | WD7500BPKT-22PK4T0 | 752 GB | 1       | 910   | 0     | 2.49   |
| WDC       | WD2500BEKT-75PVMT0 | 250 GB | 1       | 909   | 0     | 2.49   |
| Toshiba   | MQ04UBD200         | 2 TB   | 1       | 906   | 0     | 2.48   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 6       | 1575  | 3     | 2.48   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1316  | 6     | 2.47   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 8       | 898   | 0     | 2.46   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 5       | 1087  | 1     | 2.46   |
| Seagate   | ST3320620AS        | 320 GB | 6       | 1496  | 165   | 2.45   |
| HGST      | HTE725032A7E630    | 320 GB | 5       | 1224  | 12    | 2.43   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 10      | 1096  | 105   | 2.43   |
| Toshiba   | MD04ACA400         | 4 TB   | 4       | 920   | 3     | 2.43   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 3       | 1105  | 400   | 2.42   |
| WDC       | WD1600BEVT-75ZCT2  | 160 GB | 4       | 881   | 0     | 2.41   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 7       | 1178  | 3     | 2.40   |
| Samsung   | HD753LJ            | 752 GB | 4       | 1723  | 423   | 2.40   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 6       | 874   | 0     | 2.39   |
| WDC       | WD6400AAKS-65A7B0  | 640 GB | 1       | 873   | 0     | 2.39   |
| WDC       | WD1600AAJS-60B4A0  | 160 GB | 1       | 872   | 0     | 2.39   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 3       | 1742  | 13    | 2.39   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 5       | 1067  | 2     | 2.39   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 3       | 869   | 0     | 2.38   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 6       | 1057  | 2     | 2.38   |
| Seagate   | ST1000NM0011       | 1 TB   | 4       | 1690  | 8     | 2.37   |
| Seagate   | ST320410A          | 20 GB  | 1       | 2579  | 2     | 2.36   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 1       | 856   | 0     | 2.35   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 11      | 856   | 0     | 2.35   |
| Hitachi   | HDP725025GLA380    | 250 GB | 2       | 1104  | 2     | 2.34   |
| Maxtor    | STM3250310AS       | 250 GB | 4       | 927   | 1     | 2.34   |
| Hitachi   | HTS543216L9SA02    | 160 GB | 1       | 851   | 0     | 2.33   |
| WDC       | WD2500BEVT-00A23T0 | 250 GB | 1       | 851   | 0     | 2.33   |
| WDC       | WD80PURZ-85YNPY0   | 8 TB   | 1       | 851   | 0     | 2.33   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 2       | 1242  | 3     | 2.33   |
| Seagate   | ST91000640NS       | 1 TB   | 2       | 847   | 0     | 2.32   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 1       | 847   | 0     | 2.32   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 4       | 1153  | 2     | 2.32   |
| Hitachi   | HDS721050CLA662    | 500 GB | 2       | 844   | 0     | 2.32   |
| WDC       | WD10JUCT-45CYNY0   | 1 TB   | 1       | 844   | 0     | 2.31   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 1       | 842   | 0     | 2.31   |
| Seagate   | ST14000NM0018-2... | 14 TB  | 2       | 840   | 0     | 2.30   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 2       | 837   | 0     | 2.29   |
| WDC       | WD5000BEVT-22ZAT0  | 500 GB | 2       | 831   | 0     | 2.28   |
| Toshiba   | MK1032GAX          | 100 GB | 1       | 830   | 0     | 2.27   |
| HGST      | HUS726020ALA610    | 2 TB   | 2       | 822   | 0     | 2.25   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 3       | 1049  | 3     | 2.25   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 6       | 1475  | 3     | 2.24   |
| WDC       | WD1200BB-00HTA0    | 120 GB | 2       | 1633  | 347   | 2.24   |
| WDC       | WD1004FBYZ-01YCBB0 | 1 TB   | 1       | 817   | 0     | 2.24   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 1       | 816   | 0     | 2.24   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 2       | 810   | 0     | 2.22   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 2       | 810   | 0     | 2.22   |
| WDC       | WD2500JS-58NCB1    | 250 GB | 1       | 805   | 0     | 2.21   |
| Seagate   | ST500DM002-1SB10A  | 500 GB | 6       | 805   | 0     | 2.21   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 3       | 1323  | 33    | 2.21   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 5       | 803   | 0     | 2.20   |
| Toshiba   | MK4032GAX          | 40 GB  | 1       | 802   | 0     | 2.20   |
| WDC       | WD3000JS-63PDB1    | 304 GB | 1       | 802   | 0     | 2.20   |
| Lenovo    | WD2004FBYZ-23YC... | 2 TB   | 4       | 802   | 0     | 2.20   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 2       | 802   | 0     | 2.20   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 2       | 833   | 4     | 2.18   |
| Toshiba   | MG03ACA100         | 1 TB   | 10      | 792   | 0     | 2.17   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 30      | 1004  | 46    | 2.17   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 2       | 790   | 0     | 2.17   |
| WDC       | WD10JQLX-22JFGT0   | 1 TB   | 1       | 790   | 0     | 2.17   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 1       | 790   | 0     | 2.17   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 10      | 1338  | 414   | 2.16   |
| WDC       | WD5000BPKT-60PK4T0 | 500 GB | 1       | 781   | 0     | 2.14   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 10      | 779   | 0     | 2.14   |
| HGST      | HUH728080ALE600    | 8 TB   | 1       | 777   | 0     | 2.13   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 21      | 903   | 4     | 2.13   |
| Toshiba   | MK2561GSY          | 250 GB | 1       | 775   | 0     | 2.12   |
| Hitachi   | HTS727550A9E364    | 500 GB | 5       | 1035  | 233   | 2.11   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 770   | 0     | 2.11   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 9       | 1667  | 485   | 2.11   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 4       | 866   | 2     | 2.10   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 2       | 763   | 0     | 2.09   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 6       | 760   | 0     | 2.08   |
| Seagate   | ST380817AS         | 80 GB  | 4       | 760   | 0     | 2.08   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 12      | 1084  | 149   | 2.07   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 2       | 754   | 0     | 2.07   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 3       | 892   | 1     | 2.06   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 4       | 802   | 93    | 2.05   |
| Seagate   | ST31000524AS       | 1 TB   | 9       | 950   | 51    | 2.04   |
| Seagate   | ST9250410AS        | 250 GB | 7       | 799   | 34    | 2.03   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 7       | 870   | 3     | 2.02   |
| WDC       | WD5000AAKX-00U6AA0 | 500 GB | 3       | 802   | 1     | 2.02   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 1       | 734   | 0     | 2.01   |
| Seagate   | ST3160812AS        | 160 GB | 5       | 1031  | 261   | 2.00   |
| Seagate   | ST3000VN007-2AH16M | 3 TB   | 1       | 729   | 0     | 2.00   |
| WDC       | WD1600AABS-00PRA0  | 160 GB | 1       | 1458  | 1     | 2.00   |
| WDC       | WD1002FBYS-50A6B1  | 1 TB   | 1       | 727   | 0     | 1.99   |
| Samsung   | HD080HJ-P          | 80 GB  | 1       | 727   | 0     | 1.99   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 3       | 1665  | 2     | 1.99   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 4       | 726   | 0     | 1.99   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 12      | 1318  | 186   | 1.99   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 11      | 724   | 0     | 1.98   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 6       | 803   | 1     | 1.98   |
| Toshiba   | MK1002TSKB         | 1 TB   | 1       | 723   | 0     | 1.98   |
| Seagate   | ST31000424CS       | 1 TB   | 1       | 721   | 0     | 1.98   |
| Fujitsu   | MHZ2250BJ FFS G2   | 250 GB | 1       | 711   | 0     | 1.95   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 10      | 799   | 1     | 1.95   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 5       | 709   | 0     | 1.94   |
| WDC       | WD5000LPVT-75G33T0 | 500 GB | 1       | 708   | 0     | 1.94   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 1       | 707   | 0     | 1.94   |
| Hitachi   | HDS721050CLA660    | 500 GB | 5       | 1484  | 406   | 1.94   |
| Maxtor    | 6V160E0            | 160 GB | 1       | 704   | 0     | 1.93   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 6       | 702   | 0     | 1.92   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 4       | 1849  | 4     | 1.92   |
| HGST      | HUS722T2TALA600    | 2 TB   | 1       | 700   | 0     | 1.92   |
| WDC       | WD800BEVS-00RST0   | 80 GB  | 1       | 700   | 0     | 1.92   |
| Toshiba   | HDWN180            | 8 TB   | 12      | 699   | 0     | 1.92   |
| WDC       | WD20EARS-42S0XB0   | 2 TB   | 1       | 698   | 0     | 1.91   |
| Hitachi   | H7210CA30SUN1.0T   | 1 TB   | 1       | 696   | 0     | 1.91   |
| Samsung   | HD103SI            | 1 TB   | 5       | 823   | 606   | 1.91   |
| Toshiba   | DT01ACA050         | 500 GB | 23      | 913   | 13    | 1.90   |
| Seagate   | ST2000NM0011       | 2 TB   | 1       | 2080  | 2     | 1.90   |
| WDC       | WD7500BPKX-75HPJT0 | 752 GB | 1       | 693   | 0     | 1.90   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 5       | 693   | 0     | 1.90   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 1       | 692   | 0     | 1.90   |
| Seagate   | ST3320620NS        | 320 GB | 1       | 2076  | 2     | 1.90   |
| Samsung   | HM250HI            | 250 GB | 5       | 690   | 0     | 1.89   |
| WDC       | WD20NMVW-11AV3S3   | 2 TB   | 1       | 685   | 0     | 1.88   |
| Seagate   | ST2000NM0018-2F... | 2 TB   | 1       | 684   | 0     | 1.88   |
| WDC       | WD10JPVX-35JC3T0   | 1 TB   | 1       | 682   | 0     | 1.87   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 2       | 911   | 2     | 1.87   |
| MaxDig... | MD4000GSA6472E     | 4 TB   | 1       | 681   | 0     | 1.87   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 4       | 2005  | 61    | 1.86   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 1       | 678   | 0     | 1.86   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 15      | 674   | 0     | 1.85   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 7       | 663   | 0     | 1.82   |
| Hitachi   | HTS725032A9A364    | 320 GB | 3       | 1248  | 342   | 1.81   |
| Toshiba   | DT01ACA100         | 1 TB   | 39      | 757   | 28    | 1.81   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 22      | 754   | 6     | 1.81   |
| Toshiba   | HDWD120            | 2 TB   | 9       | 661   | 2     | 1.80   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 3       | 655   | 0     | 1.80   |
| Seagate   | ST380013AS         | 80 GB  | 6       | 1319  | 5     | 1.79   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 8       | 653   | 0     | 1.79   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 4       | 650   | 0     | 1.78   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 3       | 885   | 1     | 1.77   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 11      | 647   | 0     | 1.77   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 3       | 1064  | 3     | 1.77   |
| WDC       | WD1200BEVS-75UST0  | 120 GB | 1       | 645   | 0     | 1.77   |
| Hitachi   | HTS723225L9A360    | 250 GB | 1       | 644   | 0     | 1.77   |
| WDC       | WD10JPVT-08A1YT2   | 1 TB   | 1       | 642   | 0     | 1.76   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 80      | 649   | 1     | 1.74   |
| WDC       | WD7500BPVX-00JC3T0 | 752 GB | 1       | 627   | 0     | 1.72   |
| Seagate   | ST3160813AS        | 160 GB | 4       | 839   | 1     | 1.72   |
| Seagate   | ST500NM0011        | 500 GB | 3       | 2025  | 13    | 1.72   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 2       | 623   | 0     | 1.71   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 3       | 622   | 0     | 1.71   |
| HPE       | MB0500GCEHE        | 500 GB | 6       | 659   | 2     | 1.70   |
| Seagate   | ST3160811AS        | 160 GB | 1       | 620   | 0     | 1.70   |
| Apple     | HDD ST1000LM024    | 1 TB   | 1       | 617   | 0     | 1.69   |
| Seagate   | ST3000DM003-1F216N | 3 TB   | 1       | 617   | 0     | 1.69   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 2       | 616   | 0     | 1.69   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 1       | 614   | 0     | 1.68   |
| HGST      | HUS726040ALE610    | 4 TB   | 3       | 1030  | 464   | 1.68   |
| Seagate   | ST3160023AS        | 160 GB | 2       | 1239  | 3     | 1.68   |
| WDC       | WD2500AAKX-19U6AA0 | 250 GB | 1       | 613   | 0     | 1.68   |
| WDC       | WD10JPVX-00JC3T0   | 1 TB   | 5       | 613   | 0     | 1.68   |
| WDC       | WD1600JS-00NCB1    | 160 GB | 1       | 611   | 0     | 1.68   |
| WDC       | WD3001FFSX-68JNUN0 | 3 TB   | 1       | 611   | 0     | 1.67   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 66      | 1032  | 192   | 1.67   |
| WDC       | WD2500LPCX-24C6HT0 | 250 GB | 1       | 608   | 0     | 1.67   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 6       | 721   | 1     | 1.66   |
| WDC       | WD2500AAJS-40RYA0  | 250 GB | 1       | 603   | 0     | 1.65   |
| WDC       | WD2500AAKX-60U6AA0 | 250 GB | 1       | 603   | 0     | 1.65   |
| WDC       | WD2500JS-40TGB0    | 250 GB | 1       | 602   | 0     | 1.65   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 4       | 796   | 416   | 1.64   |
| Seagate   | ST12000NM0008-2... | 12 TB  | 1       | 596   | 0     | 1.63   |
| Toshiba   | HDWF180            | 8 TB   | 1       | 594   | 0     | 1.63   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 2       | 593   | 0     | 1.63   |
| Apple     | HDD HTS547550A9... | 500 GB | 2       | 639   | 14    | 1.63   |
| Toshiba   | MQ04UBF100         | 1 TB   | 1       | 592   | 0     | 1.62   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 9       | 997   | 3     | 1.62   |
| WDC       | WD2000JB-00GVC0    | 200 GB | 1       | 3539  | 5     | 1.62   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 6       | 580   | 0     | 1.59   |
| WDC       | WD4000AAKS-00TMA0  | 400 GB | 1       | 579   | 0     | 1.59   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 7       | 585   | 3     | 1.58   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 1       | 577   | 0     | 1.58   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 2       | 575   | 0     | 1.58   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 34      | 628   | 6     | 1.58   |
| HGST      | HUS726T4TALA6L1    | 4 TB   | 2       | 574   | 0     | 1.57   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 3       | 573   | 0     | 1.57   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 1       | 573   | 0     | 1.57   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 4       | 572   | 0     | 1.57   |
| Toshiba   | MG04ACA200E        | 2 TB   | 1       | 572   | 0     | 1.57   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 3       | 1376  | 3     | 1.57   |
| Samsung   | HM500JJ            | 500 GB | 1       | 571   | 0     | 1.57   |
| WDC       | WD5000BEKT-60KA9T0 | 500 GB | 1       | 569   | 0     | 1.56   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 8       | 644   | 1     | 1.56   |
| Seagate   | ST3500418AS        | 500 GB | 26      | 1304  | 122   | 1.55   |
| WDC       | WD3200BEKX-60B7WT0 | 320 GB | 1       | 564   | 0     | 1.55   |
| WDC       | WD80EDAZ-11TA3A0   | 8 TB   | 2       | 561   | 0     | 1.54   |
| Toshiba   | HDWD240            | 4 TB   | 1       | 558   | 0     | 1.53   |
| Hitachi   | HDS721050CLA362    | 500 GB | 4       | 615   | 254   | 1.53   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 4       | 556   | 0     | 1.53   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 7       | 596   | 77    | 1.52   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 7       | 553   | 0     | 1.52   |
| Fujitsu   | MHV2100BH PL       | 100 GB | 1       | 553   | 0     | 1.52   |
| WDC       | WD800BEVT-75ZCT2   | 80 GB  | 1       | 551   | 0     | 1.51   |
| Seagate   | ST2000DX001-1CM164 | 2 TB   | 1       | 548   | 0     | 1.50   |
| Samsung   | HD160JJ-P          | 160 GB | 1       | 547   | 0     | 1.50   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 13      | 542   | 0     | 1.49   |
| Samsung   | HD250HJ            | 250 GB | 2       | 1028  | 1211  | 1.49   |
| WDC       | WD5000BPVT-16HXZT3 | 500 GB | 1       | 541   | 0     | 1.48   |
| Seagate   | ST3000NM0005-1V... | 3 TB   | 3       | 540   | 0     | 1.48   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 2       | 537   | 0     | 1.47   |
| WDC       | WD3200AAKS-00V6A0  | 320 GB | 1       | 533   | 0     | 1.46   |
| WDC       | WD3000F9YZ-09N20L1 | 3 TB   | 1       | 530   | 0     | 1.45   |
| Seagate   | ST3320820AS        | 320 GB | 2       | 526   | 0     | 1.44   |
| Fujitsu   | MHT2080BH          | 80 GB  | 1       | 525   | 0     | 1.44   |
| IBM       | DBCA-204860        | 4 GB   | 1       | 522   | 0     | 1.43   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 7       | 630   | 10    | 1.43   |
| HGST      | HTE545032A7E380    | 320 GB | 3       | 521   | 0     | 1.43   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 3       | 554   | 1     | 1.43   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 12      | 615   | 81    | 1.42   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 1       | 517   | 0     | 1.42   |
| WDC       | WD5000AAKX-08ANVA0 | 500 GB | 1       | 516   | 0     | 1.42   |
| WDC       | WD10SPZX-75Z10T1   | 1 TB   | 1       | 516   | 0     | 1.41   |
| Seagate   | ST3160815AS        | 160 GB | 11      | 1339  | 100   | 1.40   |
| WDC       | WD3200BPVT-22ZEST0 | 320 GB | 2       | 509   | 0     | 1.40   |
| WDC       | WD400BD-75LRA0     | 40 GB  | 1       | 507   | 0     | 1.39   |
| WDC       | WD1600JS-23MHB0    | 160 GB | 1       | 504   | 0     | 1.38   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 1       | 502   | 0     | 1.38   |
| Seagate   | ST3750640AS        | 752 GB | 2       | 1505  | 2     | 1.38   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 1       | 501   | 0     | 1.37   |
| MediaMax  | WL1500GSA6472B     | 1.5 TB | 1       | 501   | 0     | 1.37   |
| Hitachi   | HTS725050A7E630    | 500 GB | 3       | 951   | 641   | 1.36   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 8       | 1322  | 192   | 1.36   |
| HGST      | HTS721010A9E630    | 1 TB   | 27      | 574   | 199   | 1.35   |
| WDC       | WD800AAJS-60WAA0   | 80 GB  | 1       | 1475  | 2     | 1.35   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 2       | 486   | 0     | 1.33   |
| Maxtor    | 6E040T0            | 40 GB  | 1       | 482   | 0     | 1.32   |
| WDC       | WD1200BEVS-22UST0  | 120 GB | 1       | 479   | 0     | 1.31   |
| Hitachi   | HTS545025B9A300    | 250 GB | 7       | 548   | 288   | 1.31   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 12      | 496   | 1     | 1.30   |
| Seagate   | ST6000NE0023-2E... | 6 TB   | 2       | 853   | 4     | 1.30   |
| WDC       | WD2000JS-55MHB0    | 192 GB | 1       | 470   | 0     | 1.29   |
| WDC       | WD4000FYYZ-01UL1B0 | 4 TB   | 1       | 934   | 1     | 1.28   |
| Apple     | HDD HTS541010A9... | 1 TB   | 3       | 736   | 2     | 1.28   |
| Seagate   | ST3320418AS        | 320 GB | 6       | 929   | 357   | 1.27   |
| Samsung   | HD161HJ            | 160 GB | 7       | 755   | 377   | 1.27   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 9       | 462   | 0     | 1.27   |
| Toshiba   | MK1655GSX          | 160 GB | 1       | 459   | 0     | 1.26   |
| WDC       | WD10PURX-64E5EY0   | 1 TB   | 1       | 917   | 1     | 1.26   |
| Fujitsu   | MHY2120BH          | 120 GB | 2       | 456   | 0     | 1.25   |
| HGST      | HTS541010A9E680    | 1 TB   | 15      | 527   | 275   | 1.25   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 1       | 455   | 0     | 1.25   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 11      | 455   | 0     | 1.25   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 11      | 526   | 1     | 1.24   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 4       | 507   | 2     | 1.24   |
| Hitachi   | HCC547550A9E380    | 500 GB | 1       | 445   | 0     | 1.22   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 2       | 856   | 68    | 1.22   |
| WDC       | WD4000FYYZ-05UL1B0 | 4 TB   | 1       | 444   | 0     | 1.22   |
| Toshiba   | MQ01ACF050         | 500 GB | 10      | 443   | 0     | 1.22   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 6       | 497   | 2     | 1.21   |
| Hitachi   | HDT725032VLA380    | 320 GB | 2       | 441   | 0     | 1.21   |
| Seagate   | ST9250315AS        | 250 GB | 4       | 609   | 253   | 1.21   |
| Seagate   | ST9160412ASG       | 160 GB | 1       | 440   | 0     | 1.21   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 3       | 440   | 0     | 1.21   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 2       | 434   | 0     | 1.19   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 2       | 695   | 1     | 1.19   |
| WDC       | WD7500BPKX-22HPJT0 | 752 GB | 1       | 434   | 0     | 1.19   |
| WDC       | WD2500YS-01SHB1    | 256 GB | 1       | 433   | 0     | 1.19   |
| WDC       | WD10SPCX-24HWST1   | 1 TB   | 1       | 429   | 0     | 1.18   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 36      | 549   | 4     | 1.17   |
| Seagate   | ST96812AS          | 64 GB  | 7       | 496   | 6     | 1.17   |
| Fujitsu   | MHT2080AH          | 80 GB  | 1       | 427   | 0     | 1.17   |
| WDC       | WD2000FYYZ         | 2 TB   | 2       | 1353  | 3     | 1.17   |
| Seagate   | ST3250310AS        | 250 GB | 7       | 1115  | 309   | 1.17   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 1       | 425   | 0     | 1.17   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 1       | 424   | 0     | 1.16   |
| Seagate   | ST9200420ASG       | 200 GB | 1       | 422   | 0     | 1.16   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 7       | 419   | 0     | 1.15   |
| WDC       | WD40PURZ-85AKKY0   | 4 TB   | 1       | 417   | 0     | 1.14   |
| WDC       | WD30EZRZ-00GXCB0   | 3 TB   | 1       | 417   | 0     | 1.14   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 1       | 2066  | 4     | 1.13   |
| Fujitsu   | MHY2200BH          | 200 GB | 2       | 412   | 0     | 1.13   |
| HGST      | HUS722T2TALA604    | 2 TB   | 6       | 505   | 3     | 1.13   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 5       | 410   | 0     | 1.13   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 10      | 761   | 56    | 1.12   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 4       | 408   | 0     | 1.12   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 4       | 406   | 0     | 1.11   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 2       | 406   | 0     | 1.11   |
| Maxtor    | STM3160815AS       | 160 GB | 2       | 706   | 480   | 1.11   |
| Seagate   | ST9250410ASG       | 250 GB | 2       | 404   | 0     | 1.11   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 3       | 805   | 1     | 1.10   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 2       | 402   | 0     | 1.10   |
| Hitachi   | HTS723220L9A360    | 200 GB | 1       | 401   | 0     | 1.10   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 40      | 437   | 7     | 1.10   |
| Toshiba   | HDWG180            | 8 TB   | 2       | 400   | 0     | 1.10   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 3       | 397   | 0     | 1.09   |
| WDC       | WD15EARS-00Z5B1    | 1.5 TB | 2       | 2711  | 34    | 1.09   |
| Toshiba   | HDWD130            | 3 TB   | 12      | 417   | 1     | 1.09   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 42      | 414   | 3     | 1.08   |
| WDC       | WD1600BEVT-11ZCT0  | 160 GB | 1       | 392   | 0     | 1.07   |
| WDC       | WD3200BEKT-60PVMT0 | 320 GB | 3       | 605   | 331   | 1.06   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 1       | 388   | 0     | 1.06   |
| WDC       | WD5000HHTZ-75N21V0 | 500 GB | 1       | 388   | 0     | 1.06   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 1       | 1545  | 3     | 1.06   |
| Seagate   | ST2000NE0025-2F... | 2 TB   | 2       | 385   | 0     | 1.06   |
| Seagate   | ST31500541AS       | 1.5 TB | 7       | 998   | 173   | 1.05   |
| Toshiba   | HDWD110            | 1 TB   | 16      | 383   | 0     | 1.05   |
| Toshiba   | MG04ACA600E        | 6 TB   | 2       | 382   | 0     | 1.05   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 1       | 382   | 0     | 1.05   |
| Toshiba   | MK1517GAP          | 16 GB  | 1       | 380   | 0     | 1.04   |
| HGST      | HUS726020ALE610    | 2 TB   | 2       | 380   | 0     | 1.04   |
| WDC       | WD5000AVDS-63U7B1  | 500 GB | 1       | 379   | 0     | 1.04   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 29      | 378   | 0     | 1.04   |
| WDC       | WD3200LPVX-60V0TT0 | 320 GB | 2       | 378   | 0     | 1.04   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 2       | 377   | 0     | 1.03   |
| WDC       | WD10EZEX-08Y20A0   | 1 TB   | 1       | 377   | 0     | 1.03   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 14      | 429   | 2     | 1.03   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 2       | 377   | 0     | 1.03   |
| WDC       | WD5000AZLX-60K2TA1 | 500 GB | 1       | 375   | 0     | 1.03   |
| Fujitsu   | MHZ2120BH G2       | 120 GB | 1       | 374   | 0     | 1.03   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 2       | 374   | 0     | 1.03   |
| WDC       | WD40NMZW-59GX6S1   | 4 TB   | 2       | 373   | 0     | 1.02   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 11      | 373   | 0     | 1.02   |
| Seagate   | ST9160821A         | 160 GB | 1       | 372   | 0     | 1.02   |
| WDC       | WD20EURS-63S48Y0   | 2 TB   | 1       | 3720  | 9     | 1.02   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 2       | 370   | 0     | 1.02   |
| WDC       | WD5000LPVT-80G33T2 | 500 GB | 1       | 369   | 0     | 1.01   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 2       | 369   | 0     | 1.01   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 8       | 378   | 1     | 1.01   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 4       | 619   | 259   | 1.00   |
| HPE       | MB4000GCWLV        | 4 TB   | 4       | 366   | 0     | 1.00   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 18      | 386   | 2     | 1.00   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 4       | 364   | 0     | 1.00   |
| HGST      | HTS725032A7E630    | 320 GB | 8       | 696   | 18    | 0.99   |
| Seagate   | ST3250620AS        | 250 GB | 1       | 1081  | 2     | 0.99   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 1       | 357   | 0     | 0.98   |
| Seagate   | ST500LX025-1U717D  | 500 GB | 2       | 355   | 0     | 0.97   |
| Seagate   | ST14000NM001G-2... | 14 TB  | 5       | 418   | 1     | 0.97   |
| Toshiba   | MQ01ABD075         | 752 GB | 6       | 687   | 314   | 0.97   |
| WDC       | WD10JPVT-75A1YT0   | 1 TB   | 1       | 352   | 0     | 0.97   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 2       | 351   | 0     | 0.96   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 3       | 466   | 3     | 0.96   |
| WDC       | WD2500BEVS-22UST0  | 250 GB | 4       | 374   | 2     | 0.96   |
| Seagate   | ST3120827AS        | 120 GB | 1       | 348   | 0     | 0.95   |
| Toshiba   | MN07ACA12T         | 12 TB  | 2       | 345   | 0     | 0.95   |
| Hitachi   | HDS721616PLA380    | 160 GB | 3       | 445   | 3     | 0.95   |
| Toshiba   | MK1637GSX          | 160 GB | 2       | 886   | 1     | 0.94   |
| Samsung   | HM320II            | 320 GB | 4       | 771   | 2     | 0.94   |
| WDC       | WD10EARS-003BB1    | 1 TB   | 1       | 1712  | 4     | 0.94   |
| Samsung   | HM321HI            | 320 GB | 6       | 372   | 145   | 0.94   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 10      | 414   | 2     | 0.93   |
| WDC       | WD40EFAX-68JH4N1   | 4 TB   | 1       | 340   | 0     | 0.93   |
| Toshiba   | HDWE160            | 6 TB   | 4       | 340   | 0     | 0.93   |
| WDC       | WD5000BPVT-22HXZT3 | 500 GB | 2       | 881   | 510   | 0.93   |
| Seagate   | ST980313AS         | 80 GB  | 1       | 338   | 0     | 0.93   |
| Seagate   | ST3250824AS Q      | 250 GB | 1       | 338   | 0     | 0.93   |
| Seagate   | ST3250410AS        | 250 GB | 5       | 615   | 4     | 0.92   |
| Hitachi   | HTS723232A7A364    | 320 GB | 7       | 954   | 462   | 0.91   |
| Hitachi   | HCS5C1032CLA382    | 320 GB | 1       | 1997  | 5     | 0.91   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 3       | 332   | 0     | 0.91   |
| Seagate   | ST3160212SCE       | 160 GB | 1       | 1659  | 4     | 0.91   |
| Toshiba   | MQ01UBD100         | 1 TB   | 2       | 567   | 1     | 0.91   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 27      | 329   | 0     | 0.90   |
| Seagate   | ST9250315ASG       | 250 GB | 1       | 327   | 0     | 0.90   |
| Seagate   | ST3250310NS        | 250 GB | 2       | 561   | 1     | 0.90   |
| Toshiba   | MK3259GSXP         | 320 GB | 1       | 326   | 0     | 0.89   |
| WDC       | WD20PURX-89P6ZY0   | 2 TB   | 1       | 1630  | 4     | 0.89   |
| WDC       | WD3200AVVS-63L2B0  | 320 GB | 1       | 324   | 0     | 0.89   |
| Seagate   | ST9160310AS        | 160 GB | 2       | 1388  | 2     | 0.89   |
| MediaMax  | WL2000GSA6454      | 2 TB   | 3       | 697   | 6     | 0.89   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 22      | 339   | 76    | 0.89   |
| HGST      | HTS545032A7E680    | 320 GB | 1       | 321   | 0     | 0.88   |
| WDC       | WD6400AAKS-00A7B2  | 640 GB | 1       | 320   | 0     | 0.88   |
| Toshiba   | HDWQ140            | 4 TB   | 9       | 320   | 0     | 0.88   |
| WDC       | WD5000AAVS-00G9B1  | 500 GB | 1       | 1921  | 5     | 0.88   |
| HGST      | HTS545050A7E680    | 500 GB | 12      | 370   | 86    | 0.88   |
| WDC       | WD5000LPCX-24C6HT0 | 500 GB | 5       | 319   | 0     | 0.87   |
| Seagate   | ST9500530NS 42D... | 500 GB | 1       | 637   | 1     | 0.87   |
| WDC       | WD3200BPVT-75JJ5T0 | 320 GB | 2       | 720   | 2     | 0.87   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 2       | 678   | 8     | 0.87   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 16      | 315   | 0     | 0.87   |
| Hitachi   | HTS545032B9A300    | 320 GB | 7       | 412   | 343   | 0.86   |
| Seagate   | ST2000NM000A-2J... | 2 TB   | 1       | 314   | 0     | 0.86   |
| Toshiba   | MK2546GSX          | 250 GB | 4       | 538   | 11    | 0.86   |
| Samsung   | HE161HJ            | 160 GB | 1       | 310   | 0     | 0.85   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 4       | 310   | 0     | 0.85   |
| WDC       | WD60EFRX-68TGBN1   | 6 TB   | 3       | 2362  | 7     | 0.84   |
| Seagate   | ST3120814A         | 120 GB | 1       | 3974  | 12    | 0.84   |
| Fujitsu   | MJA2250BH FFS G1   | 250 GB | 1       | 302   | 0     | 0.83   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 1       | 301   | 0     | 0.83   |
| WDC       | WD7500AAVS-00D7B0  | 752 GB | 1       | 300   | 0     | 0.82   |
| Toshiba   | DT01ACA050 LENOVO  | 500 GB | 1       | 298   | 0     | 0.82   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 3       | 296   | 0     | 0.81   |
| Seagate   | ST3250823AS        | 250 GB | 1       | 2661  | 8     | 0.81   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 1       | 293   | 0     | 0.81   |
| WDC       | WD5000LPCX-35VHAT0 | 500 GB | 1       | 293   | 0     | 0.80   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 5       | 380   | 2     | 0.80   |
| Toshiba   | MK2546GSX_200      | 200 GB | 1       | 291   | 0     | 0.80   |
| Hitachi   | HTS547550A9E384    | 500 GB | 8       | 419   | 147   | 0.80   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 5       | 426   | 51    | 0.79   |
| WDC       | WD5000AZRX-00L4HB0 | 500 GB | 1       | 288   | 0     | 0.79   |
| Toshiba   | MK3265GSXN         | 320 GB | 2       | 630   | 6     | 0.79   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 9       | 286   | 0     | 0.78   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 3       | 285   | 0     | 0.78   |
| Seagate   | ST96023AS          | 58 GB  | 1       | 1419  | 4     | 0.78   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 2       | 511   | 1     | 0.77   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 2       | 1587  | 6     | 0.77   |
| Toshiba   | MQ01ABD100         | 1 TB   | 37      | 370   | 162   | 0.76   |
| WDC       | WD10SPZX-17Z10T1   | 1 TB   | 2       | 276   | 0     | 0.76   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 11      | 1399  | 735   | 0.76   |
| WDC       | WD5000AAKX-083CA0  | 500 GB | 1       | 2482  | 8     | 0.76   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 5       | 434   | 2     | 0.75   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 18      | 324   | 77    | 0.75   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 4       | 682   | 244   | 0.75   |
| Toshiba   | MQ03UBB200         | 2 TB   | 2       | 269   | 0     | 0.74   |
| WDC       | WD10JMVW-11AJGS1   | 1 TB   | 2       | 988   | 5     | 0.74   |
| WDC       | WD1600BEVS-07RST0  | 160 GB | 1       | 267   | 0     | 0.73   |
| WDC       | WD1600BEKT-00PVMT0 | 160 GB | 1       | 264   | 0     | 0.72   |
| Hitachi   | HTS541080G9SA00    | 80 GB  | 1       | 525   | 1     | 0.72   |
| WDC       | WD5000BPVT-00HXZT3 | 500 GB | 1       | 259   | 0     | 0.71   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 7       | 259   | 0     | 0.71   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 4       | 258   | 0     | 0.71   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 2       | 257   | 0     | 0.71   |
| WDC       | WD3200BPVT-24JJ5T0 | 320 GB | 2       | 256   | 0     | 0.70   |
| Samsung   | HN-M101MBB         | 1 TB   | 2       | 255   | 0     | 0.70   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 3       | 667   | 3     | 0.70   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 1       | 255   | 0     | 0.70   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 3       | 389   | 24    | 0.70   |
| Seagate   | ST3120211AS        | 120 GB | 1       | 508   | 1     | 0.70   |
| Samsung   | HD403LJ            | 400 GB | 1       | 254   | 0     | 0.70   |
| Seagate   | ST31000340NS       | 1 TB   | 1       | 3047  | 11    | 0.70   |
| Seagate   | ST4000DM004-2U9104 | 4 TB   | 1       | 253   | 0     | 0.70   |
| Fujitsu   | MHY2250BH          | 250 GB | 1       | 253   | 0     | 0.69   |
| Toshiba   | MG06ACA800E        | 8 TB   | 7       | 251   | 0     | 0.69   |
| WDC       | WD5000LPVT-24G33T1 | 500 GB | 1       | 249   | 0     | 0.68   |
| WDC       | WD1600BEVS-08VAT2  | 160 GB | 3       | 404   | 1     | 0.68   |
| Toshiba   | MK1060GSCX         | 100 GB | 1       | 247   | 0     | 0.68   |
| WDC       | WD2500BEVT-75A23T0 | 250 GB | 1       | 246   | 0     | 0.68   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 1       | 245   | 0     | 0.67   |
| WDC       | WD40E31X-00HY4A0   | 4 TB   | 1       | 245   | 0     | 0.67   |
| WDC       | WD5000AAKS-07V0A0  | 500 GB | 1       | 244   | 0     | 0.67   |
| WDC       | WD30EFAX-68JH4N0   | 3 TB   | 1       | 244   | 0     | 0.67   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 4       | 247   | 1     | 0.67   |
| Seagate   | ST980811AS         | 80 GB  | 2       | 243   | 0     | 0.67   |
| WDC       | WD5000BPVT-22A1YT0 | 500 GB | 1       | 243   | 0     | 0.67   |
| Seagate   | ST9500325AS        | 500 GB | 20      | 488   | 202   | 0.67   |
| Seagate   | ST380215A          | 80 GB  | 1       | 242   | 0     | 0.66   |
| Seagate   | ST500LM000-1EJ162  | 500 GB | 5       | 265   | 1     | 0.66   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 8       | 434   | 109   | 0.66   |
| Hitachi   | HTS545016B9SA02    | 160 GB | 2       | 507   | 5     | 0.66   |
| HPE       | MM2000GEFRA        | 2 TB   | 6       | 239   | 0     | 0.66   |
| Toshiba   | MQ01ABD032         | 320 GB | 4       | 489   | 328   | 0.66   |
| WDC       | WD7500BPVT-80HXZT3 | 752 GB | 2       | 566   | 4     | 0.65   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 7       | 235   | 0     | 0.65   |
| Samsung   | SP0812C            | 80 GB  | 1       | 234   | 0     | 0.64   |
| WDC       | WD120EFBX-68B0EN0  | 12 TB  | 2       | 234   | 0     | 0.64   |
| Hitachi   | HTS547575A9E384    | 752 GB | 3       | 373   | 343   | 0.64   |
| Hitachi   | HTS542520K9A300    | 200 GB | 1       | 466   | 1     | 0.64   |
| Apple     | HDD ST2000DM001    | 2 TB   | 1       | 232   | 0     | 0.64   |
| Seagate   | ST750LM022 HN-M... | 752 GB | 4       | 577   | 853   | 0.63   |
| Seagate   | ST3750640NS        | 752 GB | 4       | 1709  | 528   | 0.63   |
| Samsung   | SP2514N            | 250 GB | 1       | 2529  | 10    | 0.63   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 1       | 227   | 0     | 0.62   |
| Hitachi   | HTE723225A7A364    | 250 GB | 1       | 227   | 0     | 0.62   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 1       | 678   | 2     | 0.62   |
| WDC       | WD8003FFBX-68B9AN0 | 8 TB   | 7       | 224   | 0     | 0.61   |
| Hitachi   | HTS543232L9A300    | 320 GB | 1       | 223   | 0     | 0.61   |
| WDC       | WD5000AAKS-22A7B0  | 500 GB | 1       | 2901  | 12    | 0.61   |
| Seagate   | ST9120821AS        | 120 GB | 2       | 291   | 1521  | 0.61   |
| WDC       | WD40NDZW-11MR8S1   | 4 TB   | 1       | 222   | 0     | 0.61   |
| WDC       | WD1600BEVT-22ZCT0  | 160 GB | 13      | 256   | 2     | 0.60   |
| Seagate   | ST1000LX015-1U7172 | 1 TB   | 3       | 281   | 1344  | 0.60   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 3       | 1988  | 17    | 0.60   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 18      | 572   | 384   | 0.60   |
| Apple     | HDD HTS547575A9... | 752 GB | 1       | 217   | 0     | 0.60   |
| Toshiba   | MQ01ABF050M        | 500 GB | 1       | 217   | 0     | 0.60   |
| WDC       | WD3200AAJS-60Z0A0  | 320 GB | 1       | 217   | 0     | 0.59   |
| Seagate   | ST9250827AS        | 250 GB | 5       | 448   | 241   | 0.59   |
| Toshiba   | MG08ACA16TE        | 16 TB  | 4       | 291   | 5     | 0.59   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 7       | 419   | 156   | 0.59   |
| Apple     | HDD HTS545050A7... | 500 GB | 6       | 238   | 4     | 0.59   |
| Seagate   | ST320LT020-9YG142  | 320 GB | 3       | 471   | 213   | 0.58   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 12      | 440   | 252   | 0.58   |
| WDC       | WD10SPZX-35Z10T0   | 1 TB   | 1       | 209   | 0     | 0.57   |
| WDC       | WD10SPZX-22Z10T0   | 1 TB   | 3       | 208   | 0     | 0.57   |
| Hitachi   | HDS722580VLSA80    | 82 GB  | 1       | 2494  | 11    | 0.57   |
| Fujitsu   | MHY2160BH          | 160 GB | 1       | 206   | 0     | 0.57   |
| WDC       | WD20EARX-00ZUDB0   | 2 TB   | 1       | 2266  | 10    | 0.56   |
| WDC       | WD1005FBYZ-01YCBB3 | 1 TB   | 3       | 205   | 0     | 0.56   |
| WDC       | WD3200BEVT-75ZCT2  | 320 GB | 1       | 204   | 0     | 0.56   |
| WDC       | WD4000AAKS-00C8A0  | 400 GB | 1       | 3472  | 16    | 0.56   |
| WDC       | WD6400BPVT-60HXZT1 | 640 GB | 1       | 203   | 0     | 0.56   |
| Fujitsu   | MHZ2320BH FFS G1   | 320 GB | 1       | 203   | 0     | 0.56   |
| Toshiba   | MQ01ABF032         | 320 GB | 3       | 290   | 64    | 0.56   |
| Hitachi   | HTS545032B9A302    | 320 GB | 1       | 605   | 2     | 0.55   |
| Seagate   | ST1000LM014-1EJ164 | 1 TB   | 4       | 367   | 17    | 0.55   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 9       | 581   | 634   | 0.55   |
| WDC       | WD3200AAJS-00L7A0  | 320 GB | 1       | 1806  | 8     | 0.55   |
| Samsung   | HD503HI            | 500 GB | 1       | 200   | 0     | 0.55   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 1       | 200   | 0     | 0.55   |
| WDC       | WD120EDAZ-11F3RA0  | 12 TB  | 9       | 200   | 0     | 0.55   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 3       | 199   | 0     | 0.55   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 42      | 250   | 53    | 0.54   |
| WDC       | WD3200AAVS-00ZTB0  | 320 GB | 1       | 589   | 2     | 0.54   |
| Seagate   | ST9500420AS        | 500 GB | 10      | 745   | 948   | 0.54   |
| Seagate   | ST9320421ASG       | 320 GB | 1       | 195   | 0     | 0.54   |
| WDC       | WD5000AAKS-00M9A0  | 500 GB | 1       | 391   | 1     | 0.54   |
| Toshiba   | MK1234GSX          | 120 GB | 2       | 194   | 0     | 0.53   |
| Seagate   | ST380811AS         | 80 GB  | 2       | 358   | 63    | 0.53   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 1       | 192   | 0     | 0.53   |
| WDC       | WD5000LPVX-75V0TT0 | 500 GB | 2       | 190   | 0     | 0.52   |
| Seagate   | ST3500830AS        | 500 GB | 2       | 189   | 0     | 0.52   |
| Toshiba   | MK3263GSX          | 320 GB | 1       | 1135  | 5     | 0.52   |
| Toshiba   | HDWE140            | 4 TB   | 5       | 259   | 4     | 0.52   |
| Hitachi   | HTS722020K9SA00    | 200 GB | 2       | 276   | 2     | 0.52   |
| HGST      | HTS725050A7E630    | 500 GB | 22      | 574   | 570   | 0.51   |
| WDC       | WD1600BEVT-00A23T0 | 160 GB | 2       | 187   | 0     | 0.51   |
| WDC       | WD5000LPLX-66ZNTT0 | 500 GB | 1       | 187   | 0     | 0.51   |
| Hitachi   | HTS721080G9SA00    | 80 GB  | 1       | 372   | 1     | 0.51   |
| Hitachi   | HDT721064SLA360    | 640 GB | 2       | 990   | 4     | 0.51   |
| ExcelStor | J8160S             | 160 GB | 2       | 1003  | 15    | 0.51   |
| WDC       | WD161KFGX-68AFPN0  | 16 TB  | 8       | 183   | 0     | 0.50   |
| WDC       | WD10SPSX-22A6WT0   | 1 TB   | 1       | 183   | 0     | 0.50   |
| Hitachi   | HTS545050A7E380    | 500 GB | 7       | 384   | 254   | 0.50   |
| Samsung   | HD256GJ            | 250 GB | 1       | 1274  | 6     | 0.50   |
| WDC       | WD1600JS-56MHB1    | 160 GB | 1       | 909   | 4     | 0.50   |
| WDC       | WD5000LPCX-22VHAT1 | 500 GB | 1       | 179   | 0     | 0.49   |
| WDC       | WD4000BEVT-00ZAT0  | 400 GB | 1       | 179   | 0     | 0.49   |
| WDC       | WD7500BPKX-80HPJT0 | 752 GB | 1       | 178   | 0     | 0.49   |
| WDC       | WD20SPZX-22CRAT0   | 2 TB   | 1       | 177   | 0     | 0.49   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 20      | 483   | 574   | 0.49   |
| HGST      | HTS541010B7E610    | 1 TB   | 6       | 177   | 0     | 0.49   |
| Toshiba   | MQ01ACF032         | 320 GB | 5       | 319   | 199   | 0.49   |
| Toshiba   | HDWG480UZSVB       | 8 TB   | 1       | 177   | 0     | 0.49   |
| Toshiba   | MQ01ABF050         | 500 GB | 25      | 247   | 83    | 0.49   |
| WDC       | WD5000BHTZ-50JCPV0 | 500 GB | 1       | 177   | 0     | 0.49   |
| WDC       | WD10EURX-83UY4Y0   | 1 TB   | 1       | 177   | 0     | 0.48   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 9       | 176   | 0     | 0.48   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 1       | 3354  | 18    | 0.48   |
| WDC       | WD3200BEVT-22ZCT0  | 320 GB | 4       | 241   | 4     | 0.48   |
| Seagate   | ST1000VM002-1SD102 | 1 TB   | 3       | 607   | 3     | 0.47   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 2       | 172   | 0     | 0.47   |
| HGST      | HUS722T1TALA604    | 1 TB   | 6       | 169   | 0     | 0.47   |
| Seagate   | ST9320423AS        | 320 GB | 10      | 581   | 526   | 0.46   |
| Seagate   | ST3500410AS        | 500 GB | 1       | 337   | 1     | 0.46   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 1       | 1510  | 8     | 0.46   |
| WDC       | WD80EFBX-68AZZN0   | 8 TB   | 1       | 167   | 0     | 0.46   |
| Toshiba   | HDWR180            | 8 TB   | 1       | 166   | 0     | 0.46   |
| WDC       | WD5000LPLX-60ZNTT1 | 500 GB | 2       | 212   | 1     | 0.46   |
| WDC       | WD5000LPCX-60VHAT0 | 500 GB | 3       | 550   | 466   | 0.45   |
| Seagate   | ST3500320NS        | 500 GB | 1       | 1324  | 7     | 0.45   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 14      | 297   | 291   | 0.45   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 2       | 253   | 1     | 0.45   |
| Hitachi   | HTS722010K9SA00    | 100 GB | 1       | 327   | 1     | 0.45   |
| WDC       | WD1600AAJS-75M0A0  | 160 GB | 2       | 846   | 5     | 0.45   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 2       | 161   | 0     | 0.44   |
| Fujitsu   | MJA2250BH G2       | 250 GB | 1       | 161   | 0     | 0.44   |
| Seagate   | ST3320311CS        | 320 GB | 1       | 804   | 4     | 0.44   |
| WDC       | WD800BB-00HEA0     | 80 GB  | 1       | 4322  | 26    | 0.44   |
| WDC       | WD800JB-00JJC0     | 80 GB  | 1       | 3033  | 18    | 0.44   |
| Seagate   | ST9320325AS        | 320 GB | 8       | 558   | 299   | 0.43   |
| Seagate   | ST5000LM000-2U8170 | 5 TB   | 13      | 169   | 2     | 0.43   |
| WDC       | WD1003FBYX-88 LEN  | 1 TB   | 1       | 466   | 2     | 0.43   |
| Toshiba   | MK2002TSKB         | 2 TB   | 1       | 1088  | 6     | 0.43   |
| Toshiba   | MK6034GSX          | 64 GB  | 2       | 610   | 6     | 0.43   |
| Hitachi   | HTS548040M9AT00    | 40 GB  | 2       | 452   | 2     | 0.42   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 3       | 153   | 0     | 0.42   |
| WDC       | WD2500AAKS-60L9A0  | 250 GB | 1       | 1527  | 9     | 0.42   |
| Seagate   | ST9750423AS        | 752 GB | 2       | 152   | 0     | 0.42   |
| HGST      | HTS541075A7E630    | 752 GB | 3       | 775   | 694   | 0.42   |
| WDC       | WD3200BPVT-75ZEST0 | 320 GB | 3       | 273   | 3     | 0.42   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 18      | 151   | 0     | 0.41   |
| WDC       | WD10JPVX-80JC3T0   | 1 TB   | 1       | 148   | 0     | 0.41   |
| WDC       | WD3200AAKX-753CA1  | 320 GB | 1       | 147   | 0     | 0.40   |
| Hitachi   | HTS541680J9SA00    | 80 GB  | 6       | 538   | 8     | 0.40   |
| WDC       | WD5000BPVT-08HXZT3 | 500 GB | 1       | 146   | 0     | 0.40   |
| WDC       | WD50EFRX-68L0BN1   | 5 TB   | 1       | 1314  | 8     | 0.40   |
| WDC       | WD30EZRX-22D8PB0   | 3 TB   | 1       | 875   | 5     | 0.40   |
| Toshiba   | DT01ABA300         | 3 TB   | 7       | 274   | 2     | 0.40   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 5       | 900   | 324   | 0.40   |
| WDC       | WD10SPZX-60Z10T0   | 1 TB   | 2       | 205   | 1     | 0.39   |
| WDC       | WD60EMAZ-11LW3B0   | 6 TB   | 1       | 142   | 0     | 0.39   |
| WDC       | WD5000LPVT-08G33T1 | 500 GB | 1       | 141   | 0     | 0.39   |
| WDC       | WD20EURX-63T0FY0   | 2 TB   | 2       | 1293  | 6     | 0.39   |
| Seagate   | ST4000NM0035       | 4 TB   | 1       | 141   | 0     | 0.39   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 3       | 140   | 0     | 0.38   |
| WDC       | WD5000AAKS-22V1A0  | 500 GB | 1       | 1246  | 8     | 0.38   |
| Toshiba   | MQ01ABD050         | 500 GB | 7       | 327   | 295   | 0.38   |
| WDC       | WD5000LPCX-75VHAT0 | 500 GB | 2       | 209   | 4     | 0.37   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 4       | 134   | 0     | 0.37   |
| Hitachi   | HTS547564A9E384    | 640 GB | 3       | 308   | 350   | 0.37   |
| WDC       | WD5000AZLX-00K2TA0 | 500 GB | 2       | 131   | 0     | 0.36   |
| Toshiba   | MK5065GSXF         | 500 GB | 3       | 125   | 0     | 0.34   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 3       | 125   | 0     | 0.34   |
| Seagate   | ST500LT032-1E9142  | 500 GB | 1       | 123   | 0     | 0.34   |
| WDC       | WD10JPVX-60JC3T0   | 1 TB   | 3       | 329   | 94    | 0.34   |
| WDC       | WD30EZRZ-00WN9B0   | 3 TB   | 1       | 123   | 0     | 0.34   |
| WDC       | WD400JB-00ENA0     | 40 GB  | 1       | 1722  | 13    | 0.34   |
| HPE       | MB0500EBNCR        | 500 GB | 1       | 243   | 1     | 0.33   |
| Toshiba   | MK5065GSX          | 500 GB | 1       | 361   | 2     | 0.33   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 17      | 134   | 1     | 0.33   |
| Seagate   | ST3120026A         | 120 GB | 1       | 1076  | 8     | 0.33   |
| WDC       | WD5000AVCS-632DY1  | 500 GB | 2       | 720   | 4     | 0.33   |
| WDC       | WD7500AACS-00ZJB0  | 752 GB | 1       | 1755  | 14    | 0.32   |
| Hitachi   | HTS541616J9SA00    | 160 GB | 2       | 379   | 118   | 0.32   |
| Toshiba   | MG07ACA12TE        | 12 TB  | 5       | 116   | 0     | 0.32   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 1       | 115   | 0     | 0.32   |
| WDC       | WD6400BEVT-22A0RT0 | 640 GB | 3       | 309   | 6     | 0.32   |
| Seagate   | ST500LM000-SSHD... | 500 GB | 3       | 478   | 337   | 0.31   |
| WDC       | WD10JPLX-00MBPT1   | 1 TB   | 1       | 114   | 0     | 0.31   |
| WDC       | WD40EFZX-68AWUN0   | 4 TB   | 6       | 114   | 0     | 0.31   |
| Toshiba   | MK1665GSX          | 160 GB | 1       | 114   | 0     | 0.31   |
| WDC       | WD6003FRYZ-01F0DB0 | 6 TB   | 2       | 112   | 0     | 0.31   |
| Seagate   | ST9500530NS 42D... | 500 GB | 2       | 221   | 48    | 0.31   |
| WDC       | WD1600BEVE-00UYT0  | 160 GB | 1       | 666   | 5     | 0.30   |
| HGST      | HTS545050A7E660    | 500 GB | 1       | 773   | 6     | 0.30   |
| WDC       | WD20SPZX-75UA7T0   | 2 TB   | 1       | 109   | 0     | 0.30   |
| Seagate   | ST500LM034-2GH17A  | 500 GB | 1       | 108   | 0     | 0.30   |
| WDC       | WD10SDRW-34A0XS0   | 1 TB   | 1       | 106   | 0     | 0.29   |
| WDC       | WD10SPZX-22Z10T1   | 1 TB   | 3       | 105   | 0     | 0.29   |
| WDC       | WD5000LPVX-16V0TT3 | 500 GB | 1       | 104   | 0     | 0.29   |
| Toshiba   | MQ04UBB400         | 4 TB   | 2       | 104   | 0     | 0.29   |
| WDC       | WD5000LPVX-80V0TT0 | 500 GB | 1       | 104   | 0     | 0.28   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 1       | 1338  | 12    | 0.28   |
| Seagate   | ST500VT000-1DK142  | 500 GB | 4       | 353   | 222   | 0.28   |
| HGST      | HUH721010ALE604    | 10 TB  | 2       | 102   | 0     | 0.28   |
| Seagate   | ST31000524NS       | 1 TB   | 1       | 101   | 0     | 0.28   |
| Toshiba   | MK7575GSX          | 752 GB | 1       | 604   | 5     | 0.28   |
| WDC       | WD3200BEKX-00B7WT0 | 320 GB | 1       | 702   | 6     | 0.28   |
| WDC       | WD6400AAKS-22A7B0  | 640 GB | 3       | 853   | 8     | 0.27   |
| WDC       | WD10JPVX-75JC3T0   | 1 TB   | 6       | 331   | 63    | 0.27   |
| WDC       | WD1600AAJS-60M0A0  | 160 GB | 1       | 1291  | 12    | 0.27   |
| Seagate   | ST500LM030-1RK17D  | 500 GB | 2       | 98    | 0     | 0.27   |
| WDC       | WD3200BEVT-80A0RT0 | 320 GB | 1       | 787   | 7     | 0.27   |
| Samsung   | HN-M500MBB         | 500 GB | 1       | 97    | 0     | 0.27   |
| WDC       | WD100EZAZ-11TDBA0  | 10 TB  | 1       | 97    | 0     | 0.27   |
| Toshiba   | MK2555GSX          | 250 GB | 4       | 570   | 351   | 0.26   |
| WDC       | WD20EZAZ-22L9GB0   | 2 TB   | 1       | 95    | 0     | 0.26   |
| WDC       | WD10EADS-00P8B0    | 1 TB   | 2       | 218   | 4     | 0.26   |
| WDC       | WD2500BEVT-00ZCT0  | 250 GB | 1       | 94    | 0     | 0.26   |
| Seagate   | ST980813AS         | 80 GB  | 1       | 93    | 0     | 0.26   |
| Toshiba   | MK8034GSX          | 80 GB  | 1       | 467   | 4     | 0.26   |
| WDC       | WD5000AVVS-63H0B1  | 500 GB | 1       | 466   | 4     | 0.26   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 1       | 279   | 2     | 0.25   |
| Hitachi   | HTS543225L9A300    | 250 GB | 2       | 525   | 5     | 0.25   |
| WDC       | WD3200AAJS-22B4A0  | 320 GB | 2       | 1829  | 50    | 0.25   |
| WDC       | WD10SPZX-08Z10     | 1 TB   | 4       | 92    | 0     | 0.25   |
| Seagate   | ST9160821AS        | 160 GB | 3       | 511   | 706   | 0.25   |
| WDC       | WD10JPVX-60JC3T1   | 1 TB   | 1       | 183   | 1     | 0.25   |
| WDC       | WD1600AAJS-00WAA0  | 160 GB | 2       | 100   | 1     | 0.25   |
| WDC       | WD40EZAZ-19SF3B0   | 4 TB   | 2       | 90    | 0     | 0.25   |
| Seagate   | ST500LT035-1E9G42  | 500 GB | 1       | 89    | 0     | 0.24   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 3       | 87    | 0     | 0.24   |
| Seagate   | STEC PATA          | 8 GB   | 1       | 87    | 0     | 0.24   |
| WDC       | WD10JMVW-11AJGS0   | 1 TB   | 2       | 267   | 6     | 0.24   |
| Hitachi   | HTS542580K9SA00    | 80 GB  | 1       | 85    | 0     | 0.23   |
| WDC       | WD5003ABYX-23 8... | 500 GB | 1       | 1184  | 13    | 0.23   |
| WDC       | WD10EACS-00D6B1    | 1 TB   | 1       | 750   | 8     | 0.23   |
| WDC       | WD2500AAJS-60B4A0  | 250 GB | 2       | 576   | 45    | 0.23   |
| WDC       | WD60EZRZ-00RWYB1   | 6 TB   | 1       | 904   | 10    | 0.23   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 1       | 246   | 2     | 0.23   |
| Seagate   | ST320LM000 HM321HI | 320 GB | 1       | 734   | 8     | 0.22   |
| WDC       | WD60EZRZ-22GZ5B1   | 6 TB   | 1       | 81    | 0     | 0.22   |
| HGST      | HUS722T1TALA600    | 1 TB   | 1       | 80    | 0     | 0.22   |
| Seagate   | ST4000NM002A-2H... | 4 TB   | 2       | 79    | 0     | 0.22   |
| WDC       | WUH721414ALE6L4    | 14 TB  | 1       | 79    | 0     | 0.22   |
| WDC       | WD20EZRZ-22Z5HB0   | 2 TB   | 1       | 79    | 0     | 0.22   |
| WDC       | WD80EDBZ-11B0ZA0   | 8 TB   | 1       | 77    | 0     | 0.21   |
| Toshiba   | MQ04ABF100         | 1 TB   | 14      | 103   | 2     | 0.21   |
| WDC       | WD10EADS-65M2BX    | 1 TB   | 1       | 1389  | 17    | 0.21   |
| Seagate   | ST10000NE0008-2... | 10 TB  | 1       | 76    | 0     | 0.21   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 1       | 76    | 0     | 0.21   |
| WDC       | WD5000BPVX-00JC3T0 | 500 GB | 1       | 76    | 0     | 0.21   |
| Seagate   | ST31000528AS       | 1 TB   | 9       | 695   | 150   | 0.21   |
| Toshiba   | HDWD105            | 500 GB | 4       | 919   | 143   | 0.21   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 2       | 75    | 0     | 0.21   |
| Hitachi   | HTS542516K9SA00    | 160 GB | 2       | 433   | 5     | 0.21   |
| WDC       | WD2503ABYX-01WERA0 | 256 GB | 1       | 223   | 2     | 0.20   |
| Maxtor    | STM3250820AS       | 250 GB | 1       | 444   | 5     | 0.20   |
| WDC       | WD3200BPVT-55ZEST0 | 320 GB | 1       | 142   | 1     | 0.20   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 1       | 71    | 0     | 0.20   |
| Toshiba   | MK6006GAH          | 64 GB  | 1       | 426   | 5     | 0.19   |
| Hitachi   | HCC545016B9A300    | 160 GB | 1       | 70    | 0     | 0.19   |
| WDC       | WD5000LPVX-00V0TT0 | 500 GB | 1       | 70    | 0     | 0.19   |
| WDC       | WD10EZEX-00BBHA0   | 1 TB   | 3       | 69    | 0     | 0.19   |
| Hitachi   | HTS541612J9AT00    | 120 GB | 1       | 69    | 0     | 0.19   |
| Seagate   | ST980310AS         | 80 GB  | 1       | 345   | 4     | 0.19   |
| Fujitsu   | MHZ2250BH G1       | 250 GB | 1       | 673   | 9     | 0.18   |
| Seagate   | ST9120822AS        | 120 GB | 2       | 562   | 6     | 0.18   |
| WDC       | WD20SPZX-22UA7T0   | 2 TB   | 6       | 64    | 0     | 0.18   |
| WDC       | WD3200AAJS-00YZCA0 | 320 GB | 2       | 1221  | 494   | 0.17   |
| WDC       | WD5000BEVT-24A0RT0 | 500 GB | 1       | 62    | 0     | 0.17   |
| Toshiba   | MQ02ABF050H        | 500 GB | 2       | 61    | 0     | 0.17   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 1       | 61    | 0     | 0.17   |
| Apple     | HDD HTS541010A9... | 1 TB   | 1       | 61    | 0     | 0.17   |
| Toshiba   | MK1255GSX H        | 120 GB | 3       | 216   | 44    | 0.17   |
| Toshiba   | MG09ACA18TE        | 18 TB  | 2       | 60    | 0     | 0.17   |
| WDC       | WD3200BEVT-00A0RT0 | 320 GB | 2       | 576   | 11    | 0.16   |
| WDC       | WD3200BEVT-22A23T0 | 320 GB | 1       | 521   | 8     | 0.16   |
| Hitachi   | HTS543232A7A384    | 320 GB | 6       | 280   | 529   | 0.16   |
| Hitachi   | HTS721010G9AT00    | 100 GB | 2       | 57    | 0     | 0.16   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 1       | 343   | 5     | 0.16   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 1       | 284   | 4     | 0.16   |
| WDC       | WD5000BEVT-75A0RT0 | 500 GB | 1       | 511   | 8     | 0.16   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 1       | 56    | 0     | 0.15   |
| WDC       | WD3200LPVX-75V0TT0 | 320 GB | 2       | 298   | 58    | 0.15   |
| Hitachi   | HTS541040G9SA00    | 40 GB  | 1       | 330   | 5     | 0.15   |
| Samsung   | HM160HI            | 160 GB | 7       | 466   | 190   | 0.14   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 9       | 462   | 891   | 0.14   |
| Seagate   | ST4000NM000A-2H... | 4 TB   | 1       | 52    | 0     | 0.14   |
| WDC       | WD3200BEKT-60V5T1  | 320 GB | 1       | 102   | 1     | 0.14   |
| WDC       | WD3200BEVT-60A23T0 | 320 GB | 1       | 404   | 7     | 0.14   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 2       | 2609  | 212   | 0.14   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 2       | 790   | 157   | 0.14   |
| Toshiba   | MK3261GSYN         | 320 GB | 6       | 54    | 78    | 0.13   |
| Seagate   | ST3250820AS        | 250 GB | 1       | 392   | 7     | 0.13   |
| WDC       | WD2500BEVT-08A23T1 | 250 GB | 1       | 97    | 1     | 0.13   |
| HGST      | HUS726060ALE610    | 6 TB   | 3       | 48    | 0     | 0.13   |
| Fujitsu   | MHZ2160BH G2       | 160 GB | 1       | 721   | 14    | 0.13   |
| Hitachi   | HTS541640J9SA00    | 40 GB  | 1       | 46    | 0     | 0.13   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 14      | 549   | 1007  | 0.13   |
| WDC       | WD3200BUDT-63DPZY0 | 320 GB | 1       | 46    | 0     | 0.13   |
| Samsung   | HD322GJ            | 320 GB | 1       | 412   | 8     | 0.13   |
| WDC       | WD5000LUCT-63C26Y0 | 500 GB | 1       | 45    | 0     | 0.12   |
| WDC       | WD3200BPVT-80ZEST0 | 320 GB | 1       | 406   | 8     | 0.12   |
| Hitachi   | HTS727575A9E364    | 752 GB | 1       | 1659  | 36    | 0.12   |
| WDC       | WD10SMRW-11Y43S0   | 1 TB   | 1       | 43    | 0     | 0.12   |
| WDC       | WD20EVDS-63T3B0    | 2 TB   | 1       | 385   | 8     | 0.12   |
| WDC       | WD3200BEVT-60ZCT1  | 320 GB | 2       | 237   | 5     | 0.12   |
| WDC       | WD1600AAJS-08L7A0  | 160 GB | 1       | 362   | 8     | 0.11   |
| Seagate   | ST9750420AS        | 752 GB | 1       | 742   | 18    | 0.11   |
| WDC       | WD200EB-00BHF0     | 20 GB  | 1       | 273   | 6     | 0.11   |
| WDC       | WD120EFAX-68UNTN0  | 12 TB  | 2       | 38    | 0     | 0.11   |
| HGST      | HTS545032A7E380    | 320 GB | 4       | 402   | 12    | 0.11   |
| Seagate   | ST4000LM024-2U817V | 4 TB   | 1       | 37    | 0     | 0.10   |
| Samsung   | HM251JI            | 250 GB | 2       | 75    | 14    | 0.10   |
| Seagate   | ST18000NM000J-2... | 18 TB  | 24      | 41    | 38    | 0.10   |
| Hitachi   | HTS541060G9SA00    | 64 GB  | 1       | 255   | 6     | 0.10   |
| WDC       | WD10SPZX-24Z10     | 1 TB   | 6       | 51    | 1     | 0.10   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 1       | 35    | 0     | 0.10   |
| Hitachi   | HTS541612J9SA00    | 120 GB | 6       | 669   | 45    | 0.10   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 4       | 35    | 0     | 0.10   |
| WDC       | WD2002FYPS-01U1B1  | 2 TB   | 1       | 1621  | 45    | 0.10   |
| Fujitsu   | MHS2040AT D        | 40 GB  | 1       | 1335  | 37    | 0.10   |
| WDC       | WD10SPZX-75Z10T3   | 1 TB   | 1       | 34    | 0     | 0.09   |
| Hitachi   | HTS543232L9SA00    | 320 GB | 1       | 207   | 5     | 0.09   |
| WDC       | WD4001FAEX-00MJRA0 | 4 TB   | 2       | 745   | 992   | 0.09   |
| WDC       | WD80EMZZ-00TBGA0   | 8 TB   | 1       | 33    | 0     | 0.09   |
| WDC       | WD5000AAKS-08V0A0  | 500 GB | 1       | 489   | 14    | 0.09   |
| Samsung   | HM501II            | 500 GB | 1       | 31    | 0     | 0.09   |
| Toshiba   | MK6475GSX          | 640 GB | 2       | 1418  | 48    | 0.09   |
| WDC       | WD2500BEKT-00PVMT0 | 250 GB | 1       | 31    | 0     | 0.09   |
| Seagate   | ST1000NM000A       | 1 TB   | 1       | 30    | 0     | 0.08   |
| WDC       | WD6003FZBX-00K5WB0 | 6 TB   | 3       | 84    | 1     | 0.08   |
| Seagate   | ST1000DX001-1CM162 | 1 TB   | 2       | 547   | 18    | 0.08   |
| Seagate   | ST9160411ASG       | 160 GB | 1       | 463   | 16    | 0.07   |
| Maxtor    | STM3320613AS       | 320 GB | 1       | 1639  | 61    | 0.07   |
| Seagate   | ST980210A          | 80 GB  | 1       | 26    | 0     | 0.07   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 2       | 1598  | 597   | 0.07   |
| WDC       | WD1200JS-00MHB1    | 120 GB | 1       | 437   | 17    | 0.07   |
| WDC       | WD1600BEVT-80A23T0 | 160 GB | 2       | 61    | 5     | 0.07   |
| Toshiba   | MK2552GSX          | 250 GB | 1       | 23    | 0     | 0.06   |
| Samsung   | HM320JI            | 320 GB | 3       | 208   | 9     | 0.06   |
| WDC       | WD800JD-00LSA0     | 80 GB  | 1       | 22    | 0     | 0.06   |
| Hitachi   | HTS725025A9A364    | 250 GB | 2       | 297   | 523   | 0.06   |
| Seagate   | ST20000NM007D-3... | 20 TB  | 2       | 22    | 0     | 0.06   |
| WDC       | WD10EZEX-60WN4A1   | 1 TB   | 1       | 627   | 27    | 0.06   |
| WDC       | WD3200BEVE-00A0HT0 | 320 GB | 1       | 21    | 0     | 0.06   |
| Maxtor    | 6L160M0            | 163 GB | 1       | 21    | 0     | 0.06   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 1       | 213   | 9     | 0.06   |
| HGST      | HUS726T6TALE6L1    | 6 TB   | 2       | 21    | 0     | 0.06   |
| Apple     | HDD HTS541010A9... | 1 TB   | 1       | 186   | 8     | 0.06   |
| Seagate   | ST320LT014-9YK142  | 320 GB | 1       | 402   | 19    | 0.06   |
| WDC       | WD10EARX-22N0YB0   | 1 TB   | 1       | 175   | 8     | 0.05   |
| WDC       | WD10SPCX-00KHST0   | 1 TB   | 1       | 18    | 0     | 0.05   |
| Seagate   | ST95005620AS       | 500 GB | 2       | 207   | 11    | 0.05   |
| Seagate   | ST3160812A         | 160 GB | 1       | 1893  | 107   | 0.05   |
| Seagate   | ST9320320AS        | 320 GB | 2       | 386   | 12    | 0.05   |
| Seagate   | ST8000DM004-2U9188 | 8 TB   | 1       | 17    | 0     | 0.05   |
| Seagate   | ST250LT012-1DG141  | 250 GB | 2       | 17    | 0     | 0.05   |
| WDC       | WD2500BEVT-80A23T0 | 250 GB | 1       | 426   | 24    | 0.05   |
| WDC       | WD20SPZX-00UA7T0   | 2 TB   | 1       | 16    | 0     | 0.05   |
| Seagate   | ST31500341AS       | 1.5 TB | 3       | 178   | 9     | 0.05   |
| Samsung   | SP2004C            | 200 GB | 2       | 747   | 509   | 0.04   |
| WDC       | WD2500AAKX-321CA0  | 250 GB | 1       | 369   | 22    | 0.04   |
| WDC       | WD140EFGX-68B0GN0  | 14 TB  | 2       | 15    | 0     | 0.04   |
| WDC       | WD7500LPCX-00KHST0 | 752 GB | 1       | 15    | 0     | 0.04   |
| Toshiba   | MK2561GSYN         | 250 GB | 1       | 15    | 0     | 0.04   |
| HGST      | HUS726060ALE614    | 6 TB   | 4       | 15    | 0     | 0.04   |
| Seagate   | ST16000NM000J-2... | 16 TB  | 1       | 15    | 0     | 0.04   |
| WDC       | WD3200BPVT-80JJ5T0 | 320 GB | 1       | 127   | 8     | 0.04   |
| WDC       | WD10EJRX-89N74Y0   | 1 TB   | 1       | 54    | 3     | 0.04   |
| HGST      | HUS726040ALA610    | 4 TB   | 1       | 1058  | 78    | 0.04   |
| Hitachi   | HTS542525K9A300    | 250 GB | 1       | 110   | 8     | 0.03   |
| WDC       | WD1600BPVT-11JJ5T0 | 160 GB | 1       | 11    | 0     | 0.03   |
| Toshiba   | MK3254GSY          | 320 GB | 1       | 106   | 8     | 0.03   |
| Seagate   | ST1000LM025 HN-... | 1 TB   | 1       | 117   | 9     | 0.03   |
| WDC       | WD3200AAKS-00UU3A0 | 320 GB | 1       | 103   | 8     | 0.03   |
| Samsung   | HM080HI            | 80 GB  | 1       | 627   | 56    | 0.03   |
| Seagate   | ST9250320AS        | 250 GB | 1       | 241   | 22    | 0.03   |
| WDC       | WD1600BEKT-08PVMT1 | 160 GB | 2       | 204   | 172   | 0.03   |
| Samsung   | HS082HB            | 80 GB  | 1       | 273   | 26    | 0.03   |
| Toshiba   | HDWG480            | 8 TB   | 2       | 10    | 0     | 0.03   |
| Seagate   | ST3750330NS        | 752 GB | 1       | 327   | 32    | 0.03   |
| Hitachi   | HTS543225A7A384    | 250 GB | 1       | 237   | 23    | 0.03   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 2       | 8     | 0     | 0.02   |
| Seagate   | ST3160212AS        | 160 GB | 1       | 177   | 19    | 0.02   |
| Toshiba   | MK3255GSXF         | 320 GB | 1       | 8     | 0     | 0.02   |
| WDC       | WD1600BEVS-60RST0  | 160 GB | 1       | 164   | 18    | 0.02   |
| Toshiba   | MQ03UBB300         | 3 TB   | 1       | 8     | 0     | 0.02   |
| Hitachi   | HTS543212L9A300    | 120 GB | 2       | 1802  | 550   | 0.02   |
| Toshiba   | MK5061GSY          | 500 GB | 1       | 7     | 0     | 0.02   |
| Hitachi   | HDP725016GLA380    | 160 GB | 1       | 1804  | 250   | 0.02   |
| Seagate   | ST32500NSSUN250G   | 250 GB | 2       | 6     | 0     | 0.02   |
| IBM/Hi... | IC25N080ATMR04-0   | 80 GB  | 1       | 62    | 8     | 0.02   |
| WDC       | WD2500BEVT-60A23T0 | 250 GB | 1       | 250   | 37    | 0.02   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 4       | 6     | 0     | 0.02   |
| Maxtor    | 6Y080M0            | 82 GB  | 1       | 31    | 4     | 0.02   |
| HP        | VB0160EAVEQ        | 160 GB | 1       | 718   | 116   | 0.02   |
| WDC       | WD1600BEVS-08VAT1  | 160 GB | 1       | 591   | 96    | 0.02   |
| Toshiba   | MK5061GSYN         | 500 GB | 3       | 15    | 20    | 0.02   |
| Toshiba   | MK8025GAS          | 80 GB  | 1       | 5     | 0     | 0.02   |
| Toshiba   | MQ02ABF050H-SSH... | 500 GB | 1       | 540   | 93    | 0.02   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 2       | 2203  | 676   | 0.02   |
| Toshiba   | HDWR11A            | 10 TB  | 2       | 5     | 0     | 0.01   |
| Seagate   | ST380211AS         | 80 GB  | 1       | 1418  | 277   | 0.01   |
| WDC       | WD10SPZX-24Z10T0   | 1 TB   | 2       | 209   | 22    | 0.01   |
| WDC       | WD3200BEVT-60ZCT0  | 320 GB | 1       | 133   | 29    | 0.01   |
| Seagate   | ST31000520AS       | 1 TB   | 2       | 832   | 195   | 0.01   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 1       | 1809  | 456   | 0.01   |
| Seagate   | ST3160815A         | 160 GB | 1       | 4054  | 1048  | 0.01   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 16      | 3     | 0     | 0.01   |
| Toshiba   | MK3256GSY          | 320 GB | 1       | 3     | 0     | 0.01   |
| Toshiba   | HDWL110            | 1 TB   | 1       | 3     | 0     | 0.01   |
| WDC       | WD5000AAKS-60WWPA0 | 500 GB | 1       | 798   | 241   | 0.01   |
| WDC       | WD3200BEKT-22PVMT0 | 320 GB | 1       | 969   | 300   | 0.01   |
| WDC       | WD50NMZW-59A8NS1   | 5 TB   | 1       | 3     | 0     | 0.01   |
| Hitachi   | HTS543216L9A300    | 160 GB | 1       | 1644  | 522   | 0.01   |
| Seagate   | ST3200822AS        | 200 GB | 1       | 3220  | 1081  | 0.01   |
| Toshiba   | MK3261GSY          | 320 GB | 1       | 2     | 0     | 0.01   |
| Toshiba   | MQ01ABD100V        | 1 TB   | 1       | 2     | 0     | 0.01   |
| Seagate   | ST9500420ASG       | 500 GB | 1       | 2687  | 1036  | 0.01   |
| WDC       | WD2500BEVT-24A23T0 | 250 GB | 1       | 629   | 246   | 0.01   |
| WDC       | WD1600BEKT-66F3T2  | 160 GB | 2       | 2298  | 1016  | 0.01   |
| Toshiba   | MK2018GAP          | 20 GB  | 1       | 126   | 55    | 0.01   |
| WDC       | WD3200AAJS-60M0A0  | 320 GB | 1       | 2316  | 1026  | 0.01   |
| Maxtor    | STM380815AS        | 80 GB  | 1       | 2248  | 1008  | 0.01   |
| WDC       | WD181KFGX-68AFPN0  | 18 TB  | 1       | 2     | 0     | 0.01   |
| HGST      | HTS725025A7E630    | 250 GB | 1       | 43    | 20    | 0.01   |
| Maxtor    | 6E030L0            | 32 GB  | 1       | 22    | 10    | 0.01   |
| Seagate   | ST3500514NS        | 500 GB | 1       | 205   | 103   | 0.01   |
| Maxtor    | 6Y080P0            | 82 GB  | 3       | 15    | 413   | 0.01   |
| Seagate   | ST31000333AS       | 1 TB   | 1       | 316   | 164   | 0.01   |
| Fujitsu   | MHZ2160BH FFS G1   | 160 GB | 1       | 380   | 200   | 0.01   |
| Seagate   | ST320DM000-1BD14C  | 320 GB | 1       | 1890  | 1006  | 0.01   |
| WDC       | WD40EZAZ-00SF3B0   | 4 TB   | 1       | 1     | 0     | 0.01   |
| Seagate   | ST2000DL001-9VT156 | 2 TB   | 2       | 1863  | 1006  | 0.01   |
| Seagate   | ST3160215AS        | 160 GB | 2       | 277   | 1175  | 0.01   |
| Toshiba   | MK2556GSY          | 250 GB | 1       | 1     | 0     | 0.00   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 1       | 1     | 0     | 0.00   |
| Seagate   | ST2000DM001-1E6164 | 2 TB   | 1       | 1542  | 904   | 0.00   |
| WDC       | WD6400AARS-00Y5B1  | 640 GB | 2       | 2382  | 1509  | 0.00   |
| WDC       | WD22PURZ-85B4ZY0   | 2 TB   | 4       | 1     | 0     | 0.00   |
| Samsung   | HD321KJ            | 320 GB | 2       | 1606  | 1016  | 0.00   |
| Hitachi   | HDS723015BLA642    | 1.5 TB | 1       | 1357  | 1016  | 0.00   |
| WDC       | WD2005FBYZ-01YCBB3 | 2 TB   | 2       | 1     | 0     | 0.00   |
| HGST      | HTS541075A9E680    | 752 GB | 1       | 2760  | 2177  | 0.00   |
| WDC       | WD800JD-55MUA1     | 80 GB  | 1       | 609   | 481   | 0.00   |
| Seagate   | ST3160310CS        | 160 GB | 1       | 764   | 609   | 0.00   |
| Toshiba   | MK7559GSXF         | 752 GB | 1       | 1450  | 1185  | 0.00   |
| WDC       | WD80EFZZ-68BTXN0   | 8 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | WD3200BPVT-16JJ5T0 | 320 GB | 1       | 900   | 761   | 0.00   |
| WDC       | WD2500JS-22NCB1    | 250 GB | 1       | 1197  | 1038  | 0.00   |
| WDC       | WD1600BEVS-00UST0  | 160 GB | 1       | 87    | 76    | 0.00   |
| Seagate   | ST9640320AS        | 640 GB | 2       | 1169  | 1039  | 0.00   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 1       | 1094  | 1007  | 0.00   |
| Seagate   | ST3250620NS        | 250 GB | 1       | 1057  | 1017  | 0.00   |
| Toshiba   | MK1252GSX          | 120 GB | 1       | 8     | 7     | 0.00   |
| WDC       | WD1200BEVS-07LAT0  | 120 GB | 1       | 150   | 164   | 0.00   |
| Seagate   | ST980816AS         | 80 GB  | 1       | 446   | 494   | 0.00   |
| Seagate   | ST320LM010-1KJ15C  | 320 GB | 1       | 859   | 1010  | 0.00   |
| WDC       | WD102KRYZ-01A5AB0  | 10 TB  | 2       | 0     | 0     | 0.00   |
| Hitachi   | HCC543225A7A380    | 250 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | HD642JJ            | 640 GB | 2       | 1044  | 1351  | 0.00   |
| Hitachi   | HDT722516DLAT80    | 164 GB | 1       | 1481  | 2014  | 0.00   |
| Toshiba   | MG05ACA800E        | 8 TB   | 1       | 1435  | 2073  | 0.00   |
| Seagate   | ST9160827AS        | 160 GB | 1       | 657   | 1010  | 0.00   |
| Seagate   | ST9160314AS        | 160 GB | 1       | 684   | 1062  | 0.00   |
| Hitachi   | HTS723216L9A360    | 160 GB | 1       | 646   | 1013  | 0.00   |
| Hitachi   | HDS721010DLE630    | 1 TB   | 1       | 639   | 1021  | 0.00   |
| Hitachi   | HTS725050A9A364    | 500 GB | 2       | 867   | 1465  | 0.00   |
| WDC       | WD10EADS-00M2B0    | 1 TB   | 1       | 849   | 1554  | 0.00   |
| Samsung   | HM500LI            | 500 GB | 1       | 1529  | 3036  | 0.00   |
| Fujitsu   | MHW2160BH          | 160 GB | 1       | 475   | 957   | 0.00   |
| WDC       | WD2500BEVT-35A23T0 | 250 GB | 1       | 63    | 134   | 0.00   |
| Toshiba   | HDWG440            | 4 TB   | 1       | 0     | 0     | 0.00   |
| Seagate   | ST320LT012-9WS14C  | 320 GB | 1       | 850   | 2087  | 0.00   |
| Hitachi   | HTS545050B9A300    | 500 GB | 3       | 510   | 1882  | 0.00   |
| WDC       | WD10JMVW-11AJGS2   | 1 TB   | 1       | 38    | 103   | 0.00   |
| Toshiba   | MK1059GSM          | 1 TB   | 2       | 291   | 687   | 0.00   |
| Hitachi   | HTS725032A7E630    | 320 GB | 1       | 348   | 1025  | 0.00   |
| Seagate   | ST9320325ASG       | 320 GB | 1       | 650   | 2012  | 0.00   |
| Seagate   | ST10000DM005-3A... | 10 TB  | 1       | 0     | 0     | 0.00   |
| Seagate   | ST1000NM004A-2M... | 1 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD5000B            | 500 GB | 1       | 252   | 1011  | 0.00   |
| Seagate   | ST9160412AS        | 160 GB | 2       | 254   | 1104  | 0.00   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 10      | 0     | 0     | 0.00   |
| WDC       | WD40NPZZ-00A9JT0   | 4 TB   | 1       | 0     | 0     | 0.00   |
| Toshiba   | MK2555GSXF         | 250 GB | 1       | 294   | 1456  | 0.00   |
| Samsung   | HM121HI            | 120 GB | 1       | 534   | 3029  | 0.00   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 1       | 0     | 0     | 0.00   |
| HGST      | HTS541010A7E630    | 1 TB   | 1       | 153   | 1023  | 0.00   |
| Fujitsu   | MHZ2250BH G2       | 250 GB | 1       | 148   | 1026  | 0.00   |
| Hitachi   | DK23AA-12          | 12 GB  | 1       | 4     | 31    | 0.00   |
| Samsung   | HD252HJ            | 250 GB | 1       | 173   | 1520  | 0.00   |
| Samsung   | HD082GJ            | 80 GB  | 1       | 109   | 1015  | 0.00   |
| Fujitsu   | MHV2120BH PL       | 120 GB | 1       | 0     | 0     | 0.00   |
| Hitachi   | HCS5C1050CLA382    | 500 GB | 1       | 9     | 142   | 0.00   |
| Samsung   | HM251JX            | 250 GB | 1       | 5     | 92    | 0.00   |
| Toshiba   | MQ01ABD025         | 250 GB | 1       | 168   | 3031  | 0.00   |
| Maxtor    | 6Y160M0            | 160 GB | 1       | 7     | 149   | 0.00   |
| WDC       | WD5000BPKX-60HPJT0 | 500 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | ST3160211AS        | 160 GB | 1       | 48    | 1157  | 0.00   |
| Maxtor    | 6E040L0            | 41 GB  | 1       | 20    | 1133  | 0.00   |
| Samsung   | HM250JI            | 250 GB | 1       | 16    | 1010  | 0.00   |
| Toshiba   | MK5076GSX          | 500 GB | 1       | 10    | 837   | 0.00   |
| Hitachi   | HTS721060G9AT00    | 64 GB  | 1       | 0     | 37    | 0.00   |
| Toshiba   | MK3276GSX          | 320 GB | 1       | 2     | 1008  | 0.00   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| Seagate   | Barracuda ATA V        | 1      | 1       | 5214  | 0     | 14.29  |
| Hitachi   | Deskstar 7K500         | 1      | 4       | 3376  | 0     | 9.25   |
| Seagate   | Barracuda ATA IV       | 1      | 1       | 3104  | 0     | 8.50   |
| Seagate   | Barracuda Green        | 1      | 1       | 2831  | 0     | 7.76   |
| Hitachi   | Sun Internal           | 1      | 2       | 2785  | 0     | 7.63   |
| MARVELL   | Unknown                | 1      | 1       | 2636  | 0     | 7.22   |
| WDC       | RE3                    | 8      | 16      | 2715  | 1     | 6.55   |
| Seagate   | Momentus Xt            | 1      | 1       | 2334  | 0     | 6.40   |
| Hitachi   | Deskstar 7K2000        | 1      | 2       | 2315  | 0     | 6.35   |
| WDC       | RE2-GP                 | 1      | 1       | 2306  | 0     | 6.32   |
| Seagate   | Constellation ES.2 ... | 2      | 3       | 2165  | 0     | 5.93   |
| Seagate   | Barracuda XT           | 2      | 7       | 2115  | 0     | 5.80   |
| Hitachi   | Deskstar 5K4000        | 1      | 21      | 2076  | 0     | 5.69   |
| Hitachi   | Deskstar 5K3000        | 2      | 20      | 2146  | 2     | 5.60   |
| Samsung   | SpinPoint              | 2      | 2       | 2025  | 0     | 5.55   |
| Hitachi   | Ultrastar 7K3000       | 3      | 26      | 2012  | 78    | 5.37   |
| HGST      | Ultrastar 7K4000       | 3      | 16      | 1957  | 0     | 5.36   |
| Seagate   | DB35.3                 | 1      | 1       | 1863  | 0     | 5.11   |
| Hitachi   | Deskstar 7K80          | 2      | 3       | 1830  | 0     | 5.01   |
| Hitachi   | Deskstar T7K500        | 3      | 6       | 2326  | 1     | 4.87   |
| Hitachi   | Deskstar 7K1000.B      | 5      | 11      | 2437  | 2     | 4.81   |
| Hitachi   | Deskstar 5K1000        | 2      | 2       | 1748  | 0     | 4.79   |
| Seagate   | Barracuda 7200.8       | 2      | 2       | 2924  | 4     | 4.77   |
| Seagate   | Desktop HDD            | 1      | 2       | 1714  | 0     | 4.70   |
| Hitachi   | Ultrastar A7K1000      | 3      | 5       | 2214  | 1     | 4.66   |
| HP        | Proliant HardDrive     | 5      | 12      | 2380  | 11    | 4.56   |
| Toshiba   | 2.5" HDD MK..76GSX     | 1      | 1       | 1634  | 0     | 4.48   |
| WDC       | Caviar Black           | 16     | 56      | 1893  | 23    | 4.37   |
| Hitachi   | Ultrastar A7K2000      | 5      | 34      | 2247  | 103   | 4.35   |
| Samsung   | SpinPoint F4 EG (AF)   | 1      | 20      | 2071  | 7     | 4.30   |
| Hitachi   | Deskstar E7K1000       | 1      | 3       | 3550  | 4     | 4.25   |
| Maxtor    | DiamondMax 10 (SATA... | 2      | 2       | 1537  | 0     | 4.21   |
| WDC       | AV                     | 6      | 9       | 1527  | 0     | 4.18   |
| Maxtor    | DiamondMax Plus D740X  | 1      | 3       | 2093  | 2     | 4.15   |
| Seagate   | SpinPoint F4 EG (AF)   | 1      | 2       | 1504  | 0     | 4.12   |
| Seagate   | NAS HDD                | 4      | 19      | 1588  | 2     | 4.11   |
| WDC       | Protege                | 2      | 2       | 1616  | 3     | 4.11   |
| HP        | Seagate Constellati... | 1      | 7       | 2004  | 4     | 4.09   |
| Seagate   | Desktop HDD.15         | 6      | 49      | 1571  | 22    | 4.08   |
| HGST      | Deskstar NAS           | 6      | 40      | 1623  | 21    | 4.05   |
| WDC       | Caviar SE              | 28     | 41      | 1955  | 39    | 4.02   |
| Hitachi   | Unknown                | 1      | 2       | 2248  | 6     | 4.00   |
| Seagate   | Constellation CS       | 2      | 5       | 1808  | 23    | 3.98   |
| WDC       | Green                  | 18     | 65      | 1607  | 20    | 3.96   |
| WDC       | VelociRaptor           | 10     | 16      | 1498  | 1     | 3.96   |
| Hitachi   | Deskstar 7K1000        | 2      | 10      | 1951  | 1     | 3.84   |
| HP        | 250GB SATA disk VB0... | 1      | 3       | 2037  | 2     | 3.76   |
| WDC       | RE4                    | 17     | 55      | 1436  | 19    | 3.65   |
| WDC       | Caviar                 | 5      | 6       | 2290  | 120   | 3.63   |
| WDC       | Se                     | 3      | 4       | 1321  | 0     | 3.62   |
| Samsung   | SpinPoint F3           | 2      | 15      | 1871  | 1     | 3.61   |
| WDC       | Caviar SE16            | 1      | 1       | 1317  | 0     | 3.61   |
| Toshiba   | 2.5" HDD MK..61GSYB    | 1      | 2       | 1306  | 0     | 3.58   |
| HGST      | Ultrastar He8          | 2      | 2       | 1299  | 0     | 3.56   |
| Seagate   | Terascale              | 2      | 4       | 1216  | 0     | 3.33   |
| Seagate   | Barracuda ES           | 5      | 13      | 1853  | 241   | 3.32   |
| Toshiba   | 3.5" HDD E300          | 1      | 1       | 1207  | 0     | 3.31   |
| Seagate   | Surveillance           | 5      | 7       | 1186  | 0     | 3.25   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 2      | 16      | 1155  | 0     | 3.17   |
| HGST      | Ultrastar DC HC310     | 3      | 12      | 1137  | 0     | 3.12   |
| Samsung   | SpinPoint F1 DT        | 9      | 33      | 1566  | 205   | 3.07   |
| Samsung   | SpinPoint F2 EG        | 3      | 15      | 1851  | 349   | 3.02   |
| WDC       | Caviar Green           | 26     | 51      | 1767  | 180   | 3.02   |
| Seagate   | Constellation ES.3     | 4      | 34      | 1701  | 329   | 3.02   |
| Seagate   | Constellation.2 (SATA) | 2      | 5       | 1653  | 15    | 3.00   |
| WDC       | RE                     | 12     | 25      | 1621  | 12    | 2.94   |
| Hitachi   | Deskstar P7K500        | 3      | 7       | 1564  | 42    | 2.94   |
| WDC       | Red                    | 25     | 419     | 1260  | 14    | 2.93   |
| Toshiba   | 2.5" HDD MQ01UBB       | 1      | 1       | 1067  | 0     | 2.93   |
| Seagate   | Pipeline HD 5900.2     | 5      | 24      | 1160  | 42    | 2.90   |
| Toshiba   | 2.5" HDD MQ01ABD..H    | 1      | 2       | 1041  | 0     | 2.85   |
| Seagate   | Exos 7E2               | 2      | 2       | 1032  | 0     | 2.83   |
| WDC       | Raptor                 | 3      | 3       | 1098  | 2     | 2.80   |
| Toshiba   | 3.5" MG04ACA Enterp... | 2      | 4       | 1009  | 0     | 2.76   |
| WDC       | Scorpio Black          | 22     | 37      | 1163  | 100   | 2.66   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 1       | 953   | 0     | 2.61   |
| WDC       | Caviar Blue            | 62     | 94      | 1454  | 71    | 2.57   |
| CLOVER    | Hightech Utania        | 1      | 1       | 928   | 0     | 2.54   |
| Hitachi   | CinemaStar Z5K320      | 2      | 2       | 922   | 0     | 2.53   |
| Toshiba   | 2.5" HDD MQ04UBD       | 1      | 1       | 906   | 0     | 2.48   |
| Seagate   | Archive HDD (SMR)      | 1      | 10      | 1096  | 105   | 2.43   |
| Toshiba   | 3.5" MD04ACA Enterp... | 1      | 4       | 920   | 3     | 2.43   |
| Seagate   | U6                     | 1      | 1       | 2579  | 2     | 2.36   |
| WDC       | RE2                    | 2      | 2       | 835   | 0     | 2.29   |
| Hitachi   | Deskstar 7K3000        | 3      | 9       | 2053  | 338   | 2.25   |
| Hitachi   | Deskstar 7K160         | 2      | 4       | 880   | 2     | 2.21   |
| Seagate   | Barracuda 7200.12      | 11     | 101     | 1241  | 136   | 2.20   |
| Lenovo    | RE                     | 1      | 4       | 802   | 0     | 2.20   |
| Seagate   | Barracuda 7200.7 an... | 8      | 18      | 1324  | 63    | 2.20   |
| Seagate   | Barracuda Green (AF)   | 4      | 17      | 1557  | 314   | 2.19   |
| Seagate   | Momentus 7200.3        | 4      | 5       | 980   | 5     | 2.18   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 89      | 939   | 40    | 2.17   |
| Hitachi   | Deskstar 7K1000.D      | 2      | 2       | 1109  | 511   | 2.17   |
| Seagate   | Barracuda 3.5          | 2      | 13      | 1087  | 138   | 2.15   |
| Samsung   | SpinPoint T166         | 3      | 14      | 1991  | 365   | 2.13   |
| WDC       | Ultrastar He10/12      | 5      | 48      | 770   | 0     | 2.11   |
| Seagate   | Barracuda 7200.14 (AF) | 21     | 226     | 1074  | 143   | 2.10   |
| Seagate   | Exos X14               | 2      | 3       | 758   | 0     | 2.08   |
| Seagate   | Constellation ES (S... | 3      | 8       | 1864  | 9     | 2.07   |
| WDC       | Purple                 | 13     | 23      | 850   | 1     | 2.04   |
| Hitachi   | Deskstar 7K1000.C      | 8      | 20      | 1235  | 165   | 2.03   |
| Seagate   | Barracuda 7200.9       | 12     | 18      | 1251  | 167   | 2.02   |
| Fujitsu   | MHZ BJ                 | 1      | 1       | 711   | 0     | 1.95   |
| Seagate   | Exos X12               | 1      | 5       | 709   | 0     | 1.94   |
| Hitachi   | Sun                    | 1      | 1       | 696   | 0     | 1.91   |
| Seagate   | Skyhawk                | 2      | 11      | 772   | 1     | 1.89   |
| MaxDig... | Unknown                | 1      | 1       | 681   | 0     | 1.87   |
| Maxtor    | DiamondMax 21          | 5      | 9       | 1068  | 220   | 1.86   |
| WDC       | Blue                   | 85     | 268     | 816   | 9     | 1.84   |
| Seagate   | Video 3.5 HDD          | 4      | 7       | 1115  | 67    | 1.84   |
| Seagate   | IronWolf Pro           | 5      | 11      | 730   | 1     | 1.81   |
| Seagate   | Momentus 7200.5        | 2      | 2       | 1012  | 9     | 1.81   |
| Hitachi   | Deskstar 7K4000        | 1      | 3       | 655   | 0     | 1.80   |
| Hitachi   | Travelstar 7K750       | 2      | 6       | 1139  | 200   | 1.78   |
| Seagate   | Unknown                | 4      | 4       | 646   | 0     | 1.77   |
| Toshiba   | Unknown                | 7      | 9       | 643   | 0     | 1.76   |
| Seagate   | Barracuda 7200.10      | 16     | 54      | 1229  | 245   | 1.75   |
| Samsung   | SpinPoint P80 SD       | 2      | 2       | 637   | 0     | 1.75   |
| Fujitsu   | MHW BH                 | 2      | 3       | 788   | 319   | 1.73   |
| HGST      | Travelstar 7K1000      | 2      | 30      | 702   | 179   | 1.72   |
| Hitachi   | Travelstar Z5K320      | 3      | 10      | 784   | 320   | 1.72   |
| Samsung   | SpinPoint M7           | 4      | 14      | 824   | 22    | 1.72   |
| Apple     | Momentus               | 1      | 1       | 617   | 0     | 1.69   |
| WDC       | Gold                   | 12     | 33      | 623   | 12    | 1.69   |
| Hitachi   | Ultrastar 7K4000       | 2      | 19      | 646   | 1     | 1.68   |
| HPE       | Proliant HardDrive     | 3      | 18      | 608   | 0     | 1.67   |
| ExcelStor | Jupiter                | 2      | 4       | 1009  | 8     | 1.64   |
| Hitachi   | Travelstar 7K500       | 5      | 9       | 1046  | 556   | 1.64   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 1       | 592   | 0     | 1.62   |
| Seagate   | Enterprise Capacity... | 8      | 22      | 647   | 15    | 1.59   |
| Samsung   | SpinPoint F3 EG        | 2      | 2       | 580   | 0     | 1.59   |
| Toshiba   | N300/MN NAS HDD        | 3      | 16      | 576   | 0     | 1.58   |
| WDC       | Black                  | 11     | 30      | 693   | 67    | 1.57   |
| Toshiba   | MG04ACA Enterprise HDD | 1      | 1       | 572   | 0     | 1.57   |
| Samsung   | SpinPoint MP5          | 1      | 1       | 571   | 0     | 1.57   |
| Seagate   | Barracuda LP           | 4      | 13      | 1089  | 197   | 1.53   |
| HPE       | WDC Enterprise         | 2      | 7       | 600   | 2     | 1.51   |
| Samsung   | SpinPoint S250         | 1      | 2       | 1028  | 1211  | 1.49   |
| Toshiba   | 2.5" HDD MK..65GSX     | 5      | 8       | 645   | 2     | 1.45   |
| Toshiba   | X300                   | 7      | 20      | 598   | 3     | 1.43   |
| IBM       | Travelstar 6GN         | 1      | 1       | 522   | 0     | 1.43   |
| WDC       | Black Mobile           | 15     | 32      | 593   | 1     | 1.43   |
| WDC       | Elements / My Passport | 16     | 31      | 610   | 38    | 1.42   |
| MediaMax  | WL1500                 | 1      | 1       | 501   | 0     | 1.37   |
| WDC       | Red Pro                | 11     | 51      | 521   | 40    | 1.35   |
| Seagate   | Barracuda 7200.11      | 4      | 10      | 819   | 22    | 1.32   |
| Maxtor    | DiamondMax 8s          | 1      | 1       | 482   | 0     | 1.32   |
| WDC       | AV-GP                  | 12     | 15      | 982   | 3     | 1.31   |
| Fujitsu   | MHT                    | 2      | 2       | 476   | 0     | 1.31   |
| Apple     | HGST Travelstar 5K750  | 2      | 3       | 499   | 10    | 1.28   |
| HGST      | Ultrastar HC310/320    | 1      | 9       | 462   | 0     | 1.27   |
| Hitachi   | CinemaStar C5K750      | 1      | 1       | 445   | 0     | 1.22   |
| HGST      | Ultrastar 7K6000       | 8      | 19      | 565   | 78    | 1.22   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 2      | 2       | 905   | 3     | 1.20   |
| Fujitsu   | MJA BH                 | 5      | 7       | 435   | 0     | 1.19   |
| Hitachi   | Travelstar 5K250       | 6      | 9       | 621   | 3     | 1.18   |
| HGST      | Travelstar 5K1000      | 2      | 16      | 667   | 394   | 1.17   |
| Hitachi   | Travelstar 5K100       | 4      | 4       | 615   | 3     | 1.17   |
| Hitachi   | Travelstar 5K500.B     | 8      | 27      | 616   | 410   | 1.15   |
| Toshiba   | P300                   | 5      | 42      | 507   | 15    | 1.15   |
| Seagate   | BarraCuda 3.5          | 9      | 91      | 494   | 66    | 1.13   |
| Samsung   | SpinPoint S166         | 2      | 8       | 674   | 457   | 1.11   |
| Seagate   | BarraCuda 3.5 (SMR)    | 2      | 41      | 432   | 7     | 1.09   |
| Seagate   | Laptop SSHD            | 5      | 17      | 500   | 64    | 1.07   |
| Seagate   | Barracuda 2.5 5400     | 8      | 79      | 425   | 30    | 1.07   |
| Seagate   | SpinPoint M8 (AF)      | 4      | 55      | 554   | 120   | 1.06   |
| Seagate   | IronWolf               | 11     | 105     | 408   | 1     | 1.05   |
| Seagate   | Momentus 5400.2        | 2      | 9       | 450   | 343   | 1.05   |
| Seagate   | Barracuda Compute      | 1      | 29      | 378   | 0     | 1.04   |
| WDC       | Scorpio Blue           | 74     | 131     | 482   | 30    | 1.03   |
| Hitachi   | Travelstar Z7K500      | 2      | 4       | 800   | 737   | 1.02   |
| Seagate   | SpinPoint M9T          | 1      | 8       | 378   | 1     | 1.01   |
| Fujitsu   | MHY BH                 | 4      | 6       | 366   | 0     | 1.00   |
| Samsung   | SpinPoint P120         | 3      | 4       | 1295  | 257   | 0.97   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 15      | 402   | 67    | 0.97   |
| HGST      | Travelstar Z7K500      | 5      | 37      | 702   | 345   | 0.97   |
| Toshiba   | Toshiba Client HDD     | 1      | 2       | 345   | 0     | 0.95   |
| Toshiba   | 2.5" HDD MK..37GSX     | 1      | 2       | 886   | 1     | 0.94   |
| Seagate   | DB35.2                 | 1      | 1       | 1659  | 4     | 0.91   |
| Toshiba   | 2.5" HDD MQ01UBD       | 1      | 2       | 567   | 1     | 0.91   |
| Toshiba   | 2.5" HDD MK..59GSXP    | 1      | 1       | 326   | 0     | 0.89   |
| MediaMax  | WL2000                 | 1      | 3       | 697   | 6     | 0.89   |
| Toshiba   | N300 NAS HDD           | 1      | 9       | 320   | 0     | 0.88   |
| Hitachi   | Travelstar Z7K320      | 2      | 8       | 863   | 405   | 0.88   |
| Toshiba   | 2.5" HDD MK..46GSX     | 1      | 4       | 538   | 11    | 0.86   |
| Seagate   | Momentus 7200.4        | 7      | 33      | 706   | 552   | 0.84   |
| HGST      | Ultrastar 7K2          | 4      | 14      | 345   | 2     | 0.84   |
| Toshiba   | 3.5" HDD DT01ACA       | 1      | 1       | 298   | 0     | 0.82   |
| Seagate   | Video 2.5              | 2      | 5       | 499   | 178   | 0.82   |
| Samsung   | SpinPoint M7E (AF)     | 2      | 7       | 324   | 124   | 0.81   |
| Apple     | Travelstar 5K1000      | 3      | 5       | 491   | 3     | 0.81   |
| WDC       | Unknown                | 6      | 10      | 300   | 1     | 0.81   |
| Toshiba   | 2.5" HDD               | 6      | 8       | 421   | 9     | 0.80   |
| HGST      | Travelstar Z5K500      | 5      | 21      | 415   | 52    | 0.78   |
| Seagate   | Momentus 7200.1        | 1      | 1       | 1419  | 4     | 0.78   |
| Hitachi   | Travelstar 7K320       | 4      | 4       | 484   | 254   | 0.77   |
| Seagate   | FireCuda 2.5           | 3      | 10      | 368   | 429   | 0.77   |
| Fujitsu   | MHV                    | 2      | 2       | 276   | 0     | 0.76   |
| WDC       | Blue Mobile            | 45     | 120     | 324   | 27    | 0.74   |
| Seagate   | Barracuda Pro Compute  | 2      | 19      | 312   | 73    | 0.73   |
| Seagate   | Momentus 7200.2        | 2      | 2       | 258   | 0     | 0.71   |
| Toshiba   | 2.5" HDD MQ01ABD       | 6      | 56      | 397   | 255   | 0.70   |
| Toshiba   | 2.5" HDD MQ02ABD..H    | 1      | 3       | 389   | 24    | 0.70   |
| Toshiba   | MG06ACA Enterprise ... | 1      | 7       | 251   | 0     | 0.69   |
| Hitachi   | Travelstar 5K750       | 3      | 14      | 386   | 233   | 0.67   |
| WDC       | Blue SSHD              | 1      | 1       | 245   | 0     | 0.67   |
| Samsung   | SpinPoint P80          | 1      | 1       | 234   | 0     | 0.64   |
| Apple     | Barracuda 7200.12      | 1      | 1       | 232   | 0     | 0.64   |
| WDC       | White Label            | 5      | 14      | 227   | 0     | 0.62   |
| Seagate   | Momentus 5400.6        | 8      | 38      | 552   | 332   | 0.62   |
| Seagate   | Barracuda ES.2         | 4      | 5       | 1164  | 11    | 0.59   |
| Toshiba   | MG08ACA Enterprise ... | 1      | 4       | 291   | 5     | 0.59   |
| Apple     | HGST Travelstar Z5K500 | 1      | 6       | 238   | 4     | 0.59   |
| Hitachi   | Deskstar 7K250         | 1      | 1       | 2494  | 11    | 0.57   |
| Toshiba   | 2.5" HDD MQ01ABF       | 2      | 4       | 271   | 48    | 0.57   |
| Samsung   | SpinPoint M8 (AF)      | 2      | 3       | 203   | 0     | 0.56   |
| Seagate   | Desktop SSHD           | 2      | 3       | 548   | 12    | 0.55   |
| Seagate   | Exos X16               | 2      | 23      | 209   | 1     | 0.54   |
| Seagate   | Mobile HDD             | 2      | 56      | 261   | 113   | 0.52   |
| WDC       | Internal Use HDD       | 2      | 3       | 189   | 0     | 0.52   |
| Toshiba   | 2.5" HDD MK..63GSX     | 1      | 1       | 1135  | 5     | 0.52   |
| Hitachi   | Travelstar Z5K500      | 1      | 7       | 384   | 254   | 0.50   |
| Toshiba   | 2.5" HDD MQ03UBB       | 2      | 3       | 182   | 0     | 0.50   |
| Seagate   | Constellation          | 2      | 3       | 360   | 32    | 0.50   |
| Seagate   | Momentus 5400.4        | 2      | 6       | 483   | 369   | 0.49   |
| Hitachi   | Travelstar 7K200       | 2      | 3       | 293   | 2     | 0.49   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 25      | 247   | 83    | 0.49   |
| Hitachi   | CinemaStar 5K1000      | 2      | 2       | 1003  | 74    | 0.46   |
| Seagate   | Laptop HDD             | 7      | 57      | 536   | 625   | 0.45   |
| Seagate   | Momentus 5400.3        | 4      | 8       | 439   | 267   | 0.43   |
| Hitachi   | Travelstar 5K80        | 1      | 2       | 452   | 2     | 0.42   |
| Seagate   | Momentus 5400.7 (AF)   | 1      | 2       | 152   | 0     | 0.42   |
| HGST      | Travelstar Z5K1000     | 3      | 10      | 354   | 311   | 0.42   |
| WDC       | Red Plus               | 3      | 9       | 146   | 0     | 0.40   |
| Toshiba   | 3.5" DT01ABA Deskto... | 1      | 7       | 274   | 2     | 0.40   |
| Hitachi   | Travelstar 7K100       | 4      | 5       | 406   | 9     | 0.38   |
| Hitachi   | Travelstar 5K320       | 7      | 10      | 1078  | 283   | 0.37   |
| Seagate   | Momentus 5400.5        | 4      | 6       | 689   | 9     | 0.35   |
| Seagate   | Laptop Ultrathin       | 1      | 1       | 123   | 0     | 0.34   |
| WDC       | RE4-GP                 | 3      | 5       | 1840  | 282   | 0.33   |
| Toshiba   | 2.5" HDD MK..55GSX     | 4      | 7       | 434   | 409   | 0.33   |
| Fujitsu   | MHZ BH                 | 6      | 6       | 416   | 209   | 0.32   |
| Seagate   | Barracuda SpinPoint F3 | 1      | 1       | 115   | 0     | 0.32   |
| Hitachi   | Travelstar 5K160       | 6      | 17      | 508   | 33    | 0.32   |
| Samsung   | SpinPoint F4           | 2      | 2       | 843   | 7     | 0.31   |
| WDC       | IU CB500               | 1      | 1       | 106   | 0     | 0.29   |
| Toshiba   | 2.5" HDD MQ04UBB       | 1      | 2       | 104   | 0     | 0.29   |
| Hitachi   | Travelstar 4K120       | 1      | 1       | 1338  | 12    | 0.28   |
| HGST      | Ultrastar He10         | 1      | 2       | 102   | 0     | 0.28   |
| Toshiba   | 2.5" HDD MK..34GSX     | 1      | 1       | 467   | 4     | 0.26   |
| Seagate   | Exos 7E8               | 5      | 6       | 92    | 0     | 0.25   |
| Seagate   | Ultra Mobile HDD       | 1      | 1       | 89    | 0     | 0.24   |
| Seagate   | Momentus Thin          | 3      | 13      | 459   | 668   | 0.24   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 6      | 13      | 90    | 41    | 0.23   |
| HGST      | MegaScale 4000         | 2      | 19      | 83    | 0     | 0.23   |
| Seagate   | SpinPoint M7E          | 1      | 1       | 734   | 8     | 0.22   |
| WDC       | Ultrastar DC HC530     | 1      | 1       | 79    | 0     | 0.22   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 14      | 103   | 2     | 0.21   |
| Toshiba   | Toshiba Enterprise     | 1      | 1       | 76    | 0     | 0.21   |
| Toshiba   | 1.8" HDD               | 1      | 1       | 426   | 5     | 0.19   |
| Hitachi   | CinemaStar C5K500      | 1      | 1       | 70    | 0     | 0.19   |
| Toshiba   | MG07ACA Enterprise ... | 2      | 9       | 67    | 0     | 0.18   |
| WDC       | Scorpio Blue EIDE      | 2      | 2       | 344   | 3     | 0.18   |
| Toshiba   | 2.5" HDD MK..55GSX     | 1      | 3       | 216   | 44    | 0.17   |
| Toshiba   | MG09ACA Enterprise ... | 1      | 2       | 60    | 0     | 0.17   |
| Toshiba   | 2.5" HDD MK..75GSX     | 2      | 3       | 1147  | 34    | 0.15   |
| Seagate   | Constellation ES (S... | 2      | 2       | 153   | 52    | 0.14   |
| Toshiba   | 2.5" HDD MQ02ABF..H    | 2      | 3       | 221   | 31    | 0.12   |
| Samsung   | SpinPoint M5           | 3      | 9       | 424   | 597   | 0.11   |
| Seagate   | Exos X18               | 2      | 25      | 40    | 36    | 0.10   |
| Fujitsu   | MHS AT                 | 1      | 1       | 1335  | 37    | 0.10   |
| Maxtor    | DiamondMax 22          | 1      | 1       | 1639  | 61    | 0.07   |
| Seagate   | LD25.2                 | 1      | 1       | 26    | 0     | 0.07   |
| Samsung   | SpinPoint M6           | 3      | 6       | 384   | 516   | 0.07   |
| Seagate   | Exos X20               | 1      | 2       | 22    | 0     | 0.06   |
| Maxtor    | DiamondMax 10 (ATA/... | 1      | 1       | 21    | 0     | 0.06   |
| Seagate   | Momentus XT            | 1      | 2       | 207   | 11    | 0.05   |
| Toshiba   | 2.5" HDD MK..52GSX     | 2      | 2       | 15    | 4     | 0.03   |
| Toshiba   | 2.5" HDD MK..54GSY     | 1      | 1       | 106   | 8     | 0.03   |
| Seagate   | SpinPoint M8U (USB)    | 1      | 1       | 117   | 9     | 0.03   |
| Samsung   | SpinPoint M40/60/80    | 1      | 1       | 627   | 56    | 0.03   |
| Samsung   | SpinPoint N2           | 1      | 1       | 273   | 26    | 0.03   |
| IBM/Hi... | Hitachi Travelstar ... | 1      | 1       | 62    | 8     | 0.02   |
| Toshiba   | L200                   | 1      | 1       | 3     | 0     | 0.01   |
| WDC       | Black P10              | 1      | 1       | 3     | 0     | 0.01   |
| Toshiba   | 2.5" HDD MK..56GSY     | 2      | 2       | 2     | 0     | 0.01   |
| Maxtor    | DiamondMax Plus 9      | 3      | 5       | 17    | 279   | 0.01   |
| Seagate   | Pipeline HD 5900.1     | 1      | 1       | 764   | 609   | 0.00   |
| Toshiba   | 2.5" HDD MK..59GSX     | 1      | 1       | 1450  | 1185  | 0.00   |
| Maxtor    | DiamondMax Plus 8      | 2      | 2       | 21    | 572   | 0.00   |
| Seagate   | Momentus 5400 FDE.2    | 1      | 1       | 446   | 494   | 0.00   |
| Hitachi   | Deskstar T7K250        | 1      | 1       | 1481  | 2014  | 0.00   |
| Toshiba   | MG05ACA Enterprise ... | 1      | 1       | 1435  | 2073  | 0.00   |
| Toshiba   | 2.5" HDD MK..59GSM     | 1      | 2       | 291   | 687   | 0.00   |
| Hitachi   | Travelstar DK23XX/D... | 1      | 1       | 4     | 31    | 0.00   |
| Toshiba   | 2.5" HDD MK..76GSX     | 2      | 2       | 6     | 923   | 0.00   |

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
| MARVELL     | 1      | 1       | 2636  | 0     | 7.22   |
| HP          | 7      | 22      | 2213  | 7     | 4.30   |
| Hitachi     | 125    | 365     | 1400  | 142   | 2.86   |
| CLOVER      | 1      | 1       | 928   | 0     | 2.54   |
| Samsung     | 50     | 162     | 1357  | 211   | 2.38   |
| WDC         | 591    | 1732    | 1060  | 28    | 2.37   |
| Lenovo      | 1      | 4       | 802   | 0     | 2.20   |
| HGST        | 47     | 247     | 826   | 125   | 1.90   |
| MaxDigital  | 1      | 1       | 681   | 0     | 1.87   |
| ExcelStor   | 2      | 4       | 1009  | 8     | 1.64   |
| Seagate     | 290    | 1512    | 834   | 136   | 1.63   |
| Maxtor      | 16     | 24      | 885   | 191   | 1.63   |
| HPE         | 5      | 25      | 605   | 1     | 1.62   |
| IBM         | 1      | 1       | 522   | 0     | 1.43   |
| Toshiba     | 112    | 446     | 557   | 73    | 1.23   |
| MediaMax    | 2      | 4       | 648   | 5     | 1.01   |
| Fujitsu     | 23     | 28      | 488   | 81    | 0.99   |
| Apple       | 8      | 16      | 389   | 4     | 0.86   |
| IBM/Hitachi | 1      | 1       | 62    | 8     | 0.02   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| OCZ       | VERTEX2            | 64 GB  | 1       | 3103  | 0     | 8.50   |
| Crucial   | M4-CT064M4SSD3     | 64 GB  | 1       | 2802  | 0     | 7.68   |
| Micron    | P400e-MTFDDAK10... | 100 GB | 1       | 2774  | 0     | 7.60   |
| Transcend | TS64GMSA340        | 64 GB  | 1       | 2730  | 0     | 7.48   |
| Kingston  | SVP180S2128G       | 128 GB | 1       | 2596  | 0     | 7.11   |
| Corsair   | Force 3 SSD        | 240 GB | 2       | 2571  | 0     | 7.04   |
| Samsung   | MMCRE28G5MXP-0VB   | 128 GB | 1       | 2567  | 0     | 7.03   |
| Intel     | SSDSA2SH032G1SB    | 32 GB  | 1       | 2546  | 0     | 6.98   |
| G.Skill   | FM-25S3-120GBP3    | 120 GB | 1       | 2532  | 0     | 6.94   |
| Samsung   | MZ7TE128HMGR-00000 | 128 GB | 1       | 2484  | 0     | 6.81   |
| Intel     | SSDMCEAC120B3      | 120 GB | 2       | 2427  | 0     | 6.65   |
| OCZ       | VERTEX3 MI         | 240 GB | 1       | 2426  | 0     | 6.65   |
| Intel     | SSDSC2BA200G4      | 200 GB | 1       | 2420  | 0     | 6.63   |
| Intel     | SSDSC2BB240G4      | 240 GB | 1       | 2399  | 0     | 6.57   |
| Intel     | TK0080GDSAE        | 80 GB  | 1       | 2368  | 0     | 6.49   |
| Apple     | SSD SM512E         | 500 GB | 2       | 2341  | 0     | 6.41   |
| Intel     | SSDSC2BB160G4      | 160 GB | 2       | 2314  | 0     | 6.34   |
| OCZ       | AGILITY            | 32 GB  | 2       | 2269  | 0     | 6.22   |
| OCZ       | VECTOR             | 256 GB | 1       | 2265  | 0     | 6.21   |
| Intel     | SSDSC2BB240G6      | 240 GB | 3       | 2265  | 0     | 6.21   |
| Samsung   | MZ7GE480HMHP-00003 | 480 GB | 1       | 2235  | 0     | 6.12   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 2       | 2205  | 0     | 6.04   |
| HPE       | MK0400GCTZA        | 400 GB | 2       | 2183  | 0     | 5.98   |
| Lenovo    | SSDSC2BB120G6N ... | 120 GB | 1       | 2171  | 0     | 5.95   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 1       | 2166  | 0     | 5.94   |
| Micron    | P400m100-MTFDDA... | 100 GB | 1       | 2158  | 0     | 5.91   |
| OCZ       | SOLID3             | 120 GB | 1       | 2144  | 0     | 5.87   |
| Intel     | SSDMAEMC080G2      | 80 GB  | 1       | 2140  | 0     | 5.86   |
| Intel     | SSDSA2BZ100G3      | 100 GB | 1       | 2121  | 0     | 5.81   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 5       | 2082  | 0     | 5.70   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 1       | 2045  | 0     | 5.60   |
| Mushkin   | MKNSSDCR60GB-DX    | 64 GB  | 1       | 2029  | 0     | 5.56   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 2       | 2007  | 0     | 5.50   |
| Corsair   | Force GT           | 240 GB | 1       | 1999  | 0     | 5.48   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 2       | 2627  | 1     | 5.48   |
| HP        | VK0800GDJYA        | 800 GB | 1       | 1986  | 0     | 5.44   |
| Intel     | SSDSC2BF120A5      | 120 GB | 1       | 1960  | 0     | 5.37   |
| Micron    | M600_MTFDDAT128MBF | 128 GB | 1       | 1944  | 0     | 5.33   |
| Samsung   | MZMTE256HMHP-00007 | 256 GB | 1       | 1941  | 0     | 5.32   |
| SanDisk   | SDSA6AM-008G-1006  | 8 GB   | 1       | 1932  | 0     | 5.30   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 1       | 1923  | 0     | 5.27   |
| ADATA     | SP310              | 32 GB  | 2       | 1914  | 0     | 5.25   |
| OCZ       | VERTEX PLUS        | 64 GB  | 1       | 1901  | 0     | 5.21   |
| Micron    | M600_MTFDDAK128MBF | 128 GB | 1       | 1854  | 0     | 5.08   |
| Transcend | TS32GMSA740        | 32 GB  | 1       | 1825  | 0     | 5.00   |
| SanDisk   | PU1000064GBATSSD   | 64 GB  | 1       | 1818  | 0     | 4.98   |
| Samsung   | SSD PB22-JS3 TM    | 64 GB  | 1       | 1801  | 0     | 4.94   |
| Patriot   | Ignite M3          | 120 GB | 1       | 1798  | 0     | 4.93   |
| SanDisk   | SDSA5AK-008G-1006  | 8 GB   | 1       | 1794  | 0     | 4.92   |
| Intel     | SSDSC2BP240G4      | 240 GB | 3       | 1783  | 0     | 4.89   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 14      | 1837  | 146   | 4.88   |
| OCZ       | AGILITY4           | 256 GB | 1       | 1775  | 0     | 4.87   |
| Samsung   | SSD 840 EVO        | 120 GB | 30      | 1989  | 14    | 4.85   |
| Intel     | SSDSC2CW180A3      | 180 GB | 1       | 1763  | 0     | 4.83   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 2       | 1756  | 0     | 4.81   |
| Samsung   | MZ7WD480HAGM-000D3 | 480 GB | 1       | 1752  | 0     | 4.80   |
| China     | SATA SSD           | 8 GB   | 1       | 1752  | 0     | 4.80   |
| Toshiba   | TR150              | 120 GB | 1       | 1746  | 0     | 4.79   |
| Intel     | SSDSC2BB300G4      | 304 GB | 1       | 1746  | 0     | 4.78   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 1       | 1736  | 0     | 4.76   |
| Toshiba   | THNSNH512GBST      | 512 GB | 1       | 1700  | 0     | 4.66   |
| Intel     | SSDSC2BB240G7      | 240 GB | 1       | 1698  | 0     | 4.65   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 12      | 1683  | 0     | 4.61   |
| Intel     | SSDSA2CW120G3      | 120 GB | 7       | 1679  | 0     | 4.60   |
| Toshiba   | THNSNX032GTNT M... | 32 GB  | 1       | 1665  | 0     | 4.56   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 1       | 1656  | 0     | 4.54   |
| SanDisk   | SDSSDX120GG25      | 120 GB | 1       | 1642  | 0     | 4.50   |
| OCZ       | VERTEX4            | 256 GB | 3       | 1605  | 0     | 4.40   |
| Transcend | TS8GSSD500         | 8 GB   | 1       | 1604  | 0     | 4.40   |
| Samsung   | SSD 830 Series     | 256 GB | 3       | 1575  | 0     | 4.32   |
| ADATA     | SP310              | 64 GB  | 1       | 1573  | 0     | 4.31   |
| SanDisk   | SDSSDH2128G        | 128 GB | 1       | 1572  | 0     | 4.31   |
| SanDisk   | SDSSDXP480G        | 480 GB | 2       | 1552  | 0     | 4.25   |
| ADATA     | SP920SS            | 128 GB | 1       | 1542  | 0     | 4.22   |
| Intel     | SSDMCEAC030B3      | 32 GB  | 6       | 1529  | 0     | 4.19   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 1       | 1526  | 0     | 4.18   |
| Apple     | SSD TS128C         | 121 GB | 3       | 1519  | 0     | 4.16   |
| Kingston  | SHSS37A120G        | 120 GB | 1       | 1511  | 0     | 4.14   |
| ADATA     | SP310              | 128 GB | 1       | 1488  | 0     | 4.08   |
| Samsung   | MZMTD128HAFV-000L1 | 128 GB | 1       | 1487  | 0     | 4.08   |
| Samsung   | MZ-5EA2000-0D3     | 200 GB | 4       | 1481  | 0     | 4.06   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 3       | 1479  | 0     | 4.05   |
| Samsung   | MZMPC256HBGJ-000L1 | 256 GB | 1       | 1470  | 0     | 4.03   |
| Intel     | SSDSC2BB080G6      | 80 GB  | 2       | 1466  | 0     | 4.02   |
| SanDisk   | SD7SF6S512G1122    | 512 GB | 1       | 1464  | 0     | 4.01   |
| Innodisk  | Corp. - mSATA 3ME4 | 16 GB  | 1       | 1456  | 0     | 3.99   |
| Samsung   | MZYTY128HDHP-000L2 | 128 GB | 1       | 1456  | 0     | 3.99   |
| OCZ       | VERTEX3 MI         | 120 GB | 2       | 2104  | 1     | 3.97   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 1       | 1449  | 0     | 3.97   |
| OCZ       | AGILITY3           | 120 GB | 8       | 1466  | 151   | 3.93   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 2       | 1431  | 0     | 3.92   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 1       | 1425  | 0     | 3.91   |
| Micron    | M550_MTFDDAT256MAY | 256 GB | 1       | 1421  | 0     | 3.89   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 2       | 1416  | 0     | 3.88   |
| Seagate   | XF1230-1A0240      | 240 GB | 2       | 1416  | 0     | 3.88   |
| Team      | L3 EVO SSD         | 120 GB | 1       | 1416  | 0     | 3.88   |
| Kingston  | SVP200S3120G       | 120 GB | 2       | 1411  | 0     | 3.87   |
| Intel     | SSDSC2CT180A3      | 180 GB | 4       | 1895  | 1     | 3.86   |
| Crucial   | FCCT128M4SSD1      | 128 GB | 2       | 1406  | 0     | 3.85   |
| Intel     | SSDSC2CT180A4      | 180 GB | 3       | 1870  | 1     | 3.82   |
| Intel     | SSDSC2BA400G3      | 400 GB | 1       | 1392  | 0     | 3.82   |
| Toshiba   | THNSNJ128GCSY      | 128 GB | 2       | 1388  | 0     | 3.80   |
| Plextor   | PX-512M5Pro        | 512 GB | 1       | 1381  | 0     | 3.79   |
| HP        | FK0032CAAZP        | 32 GB  | 3       | 1371  | 0     | 3.76   |
| Samsung   | SSD PB22-JS3 2.5"  | 128 GB | 1       | 1365  | 0     | 3.74   |
| SanDisk   | SSD U100           | 8 GB   | 1       | 1365  | 0     | 3.74   |
| Innodisk  | Corp. DRPS-08GJ... | 8 GB   | 1       | 1364  | 0     | 3.74   |
| Seagate   | ST240HM000-1G5152  | 240 GB | 2       | 1356  | 0     | 3.72   |
| Lite-On   | PH5-CE120          | 120 GB | 1       | 1355  | 0     | 3.71   |
| ADATA     | SP900              | 64 GB  | 3       | 1342  | 0     | 3.68   |
| Samsung   | SSD 840 EVO        | 500 GB | 7       | 1414  | 120   | 3.65   |
| Samsung   | SSD PM830 mSATA    | 64 GB  | 1       | 1306  | 0     | 3.58   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 3       | 1550  | 341   | 3.57   |
| Smart     | SGMST3D64GBM01EMC  | 64 GB  | 1       | 1298  | 0     | 3.56   |
| Kingston  | SVP200S37A60G      | 64 GB  | 5       | 1297  | 0     | 3.56   |
| Micro ... | G2 series          | 64 GB  | 1       | 1297  | 0     | 3.55   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 9       | 1537  | 112   | 3.55   |
| Superm... | SSD                | 128 GB | 1       | 1295  | 0     | 3.55   |
| Samsung   | MZ7LM240HCGR-0E003 | 240 GB | 2       | 1295  | 0     | 3.55   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 1       | 1283  | 0     | 3.52   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 14      | 1279  | 0     | 3.51   |
| Corsair   | Force GS           | 128 GB | 2       | 1279  | 0     | 3.51   |
| HPE       | MK000480GWCEV      | 480 GB | 2       | 1275  | 0     | 3.49   |
| HPE       | MK000960GWCFA      | 960 GB | 2       | 1275  | 0     | 3.49   |
| SK hynix  | SC300 SATA         | 512 GB | 1       | 1266  | 0     | 3.47   |
| Seagate   | XF1230-1A0480      | 480 GB | 2       | 1266  | 0     | 3.47   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 3       | 1430  | 1     | 3.45   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 2       | 1260  | 0     | 3.45   |
| Samsung   | MZNTY256HDHP-000L2 | 256 GB | 1       | 1258  | 0     | 3.45   |
| Samsung   | SSD 830 Series     | 128 GB | 13      | 1240  | 0     | 3.40   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 1       | 1235  | 0     | 3.38   |
| Toshiba   | THNSNH128GBST      | 128 GB | 3       | 1234  | 0     | 3.38   |
| OCZ       | AGILITY3           | 128 GB | 1       | 1233  | 0     | 3.38   |
| Intel     | SSDMCEAW180A4      | 180 GB | 1       | 1230  | 0     | 3.37   |
| Samsung   | SSD CM871 2.5 7mm  | 128 GB | 2       | 1228  | 0     | 3.37   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 2       | 1224  | 0     | 3.35   |
| Samsung   | SSD 850 PRO        | 128 GB | 13      | 1215  | 0     | 3.33   |
| Samsung   | MZ7PC128HAFU-000H1 | 128 GB | 1       | 1208  | 0     | 3.31   |
| Intel     | SSDSC2BA400G4      | 400 GB | 2       | 1205  | 0     | 3.30   |
| SanDisk   | Ultra II           | 960 GB | 2       | 1202  | 0     | 3.29   |
| Samsung   | SG9XCS1F50GMIBM... | 50 GB  | 1       | 1184  | 0     | 3.24   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 3       | 1180  | 0     | 3.24   |
| BlueRay   | SDM03II-HRM        | 16 GB  | 1       | 1177  | 0     | 3.23   |
| Intel     | SSDSC2BB960G7R     | 960 GB | 6       | 1177  | 0     | 3.23   |
| Superm... | SSD                | 16 GB  | 1       | 1176  | 0     | 3.22   |
| Samsung   | SSD PB22-JS3 FD... | 128 GB | 2       | 1176  | 0     | 3.22   |
| Dell      | SSDSCKJB120G7R     | 120 GB | 2       | 1173  | 0     | 3.22   |
| Intel     | SSDMCEAW080A4      | 80 GB  | 1       | 1170  | 0     | 3.21   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 1154  | 0     | 3.16   |
| Samsung   | SSD 840 Series     | 120 GB | 19      | 1245  | 55    | 3.16   |
| Samsung   | SSD 840 PRO Series | 128 GB | 18      | 1257  | 90    | 3.12   |
| Samsung   | SSD 840 Series     | 250 GB | 7       | 1128  | 0     | 3.09   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 3       | 1128  | 0     | 3.09   |
| Samsung   | SSD 840 EVO 1TB... | 1 TB   | 1       | 1127  | 0     | 3.09   |
| Toshiba   | THNSF8120CCSE      | 120 GB | 1       | 1126  | 0     | 3.09   |
| Intel     | SSDSA2CW160G3      | 160 GB | 4       | 1125  | 0     | 3.08   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 2       | 1125  | 0     | 3.08   |
| SanDisk   | SD6SF1M128G        | 128 GB | 1       | 1121  | 0     | 3.07   |
| Intel     | SSDSC2BB120G4      | 120 GB | 17      | 1189  | 1     | 3.06   |
| Kingston  | SM2280S3G2120G     | 120 GB | 1       | 1117  | 0     | 3.06   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 2       | 1117  | 0     | 3.06   |
| Patriot   | Flare              | 64 GB  | 2       | 1107  | 0     | 3.03   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 1105  | 0     | 3.03   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 3       | 1105  | 0     | 3.03   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 2       | 1226  | 1     | 3.03   |
| Innodisk  | M.2 (S42) 3ME4     | 64 GB  | 1       | 1101  | 0     | 3.02   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 5       | 1101  | 0     | 3.02   |
| ADATA     | SP600              | 32 GB  | 2       | 1097  | 0     | 3.01   |
| Intel     | SSDSC2BB120G4I ... | 120 GB | 1       | 1092  | 0     | 2.99   |
| V-GeN     | V-GEN11SM18EG120GB | 120 GB | 1       | 1084  | 0     | 2.97   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 5       | 1084  | 0     | 2.97   |
| HP        | VK0480GECQP        | 480 GB | 1       | 1083  | 0     | 2.97   |
| OCZ       | VERTEX3            | 64 GB  | 4       | 1591  | 8     | 2.96   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 1       | 1080  | 0     | 2.96   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 1       | 2157  | 1     | 2.96   |
| SanDisk   | SD7SB6S256G1001    | 256 GB | 1       | 1077  | 0     | 2.95   |
| SanDisk   | SDSA6PM-064G-1006  | 64 GB  | 2       | 1064  | 0     | 2.92   |
| Kingston  | SKC400S37512G      | 512 GB | 2       | 1059  | 0     | 2.90   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 2       | 1056  | 0     | 2.90   |
| Apple     | SSD SD512E         | 500 GB | 1       | 1056  | 0     | 2.89   |
| Intel     | SSDSC2CW240A3      | 240 GB | 6       | 1045  | 0     | 2.86   |
| Kingston  | SNV425S2128GB      | 128 GB | 3       | 2111  | 6     | 2.86   |
| BIWIN     | SSD                | 120 GB | 1       | 1041  | 0     | 2.85   |
| Patriot   | Pyro               | 64 GB  | 1       | 1039  | 0     | 2.85   |
| KingSpec  | NT-64              | 64 GB  | 1       | 1033  | 0     | 2.83   |
| Intel     | SSDSC2KB240G7      | 240 GB | 3       | 1031  | 0     | 2.82   |
| Faspeed   | H5-60G PLUS        | 64 GB  | 1       | 1025  | 0     | 2.81   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 1       | 1012  | 0     | 2.77   |
| Samsung   | SSD 830 Series     | 64 GB  | 3       | 1010  | 0     | 2.77   |
| Crucial   | CT250MX200SSD1     | 250 GB | 5       | 1078  | 1     | 2.76   |
| Patriot   | Blaze              | 64 GB  | 2       | 1006  | 0     | 2.76   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 5       | 1002  | 0     | 2.75   |
| Mushkin   | MKNSSDEC120GB      | 120 GB | 1       | 1001  | 0     | 2.74   |
| ADATA     | SX930              | 240 GB | 1       | 1001  | 0     | 2.74   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 5       | 998   | 0     | 2.73   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 1       | 995   | 0     | 2.73   |
| Toshiba   | THNSFJ256GDNU      | 256 GB | 2       | 986   | 0     | 2.70   |
| PNY       | CS1311 240GB SSD   | 240 GB | 4       | 985   | 0     | 2.70   |
| Goodram   | SSD                | 240 GB | 4       | 983   | 0     | 2.70   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 6       | 981   | 0     | 2.69   |
| Silico... | SP-mSATA-64G       | 64 GB  | 1       | 976   | 0     | 2.68   |
| Corsair   | Force 3 SSD        | 180 GB | 1       | 2914  | 2     | 2.66   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 3       | 969   | 0     | 2.66   |
| SanDisk   | SD9SB8W256G1122    | 256 GB | 1       | 961   | 0     | 2.63   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 1       | 959   | 0     | 2.63   |
| CFD       | CSSD-S6M256CG3VZ   | 256 GB | 1       | 957   | 0     | 2.62   |
| Innodisk  | DEMSR- 32GB mSA... | 32 GB  | 1       | 956   | 0     | 2.62   |
| Crucial   | CT128M550SSD1      | 128 GB | 2       | 1528  | 2     | 2.62   |
| OCZ       | VERTEX4            | 128 GB | 5       | 1130  | 1     | 2.61   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 4       | 1231  | 522   | 2.60   |
| SanDisk   | X600 2.5 7MM SATA  | 256 GB | 1       | 947   | 0     | 2.59   |
| SuperM... | SSD                | 16 GB  | 1       | 944   | 0     | 2.59   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 5       | 936   | 0     | 2.56   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 2       | 935   | 0     | 2.56   |
| AMD       | R3SL120G           | 120 GB | 3       | 933   | 0     | 2.56   |
| Samsung   | SSD 750 EVO        | 120 GB | 10      | 916   | 0     | 2.51   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 2       | 911   | 0     | 2.50   |
| Samsung   | SSD 750 EVO        | 250 GB | 11      | 903   | 0     | 2.48   |
| Origin... | mSATA MLC800 SSD   | 128 GB | 1       | 900   | 0     | 2.47   |
| Lite-On   | LCS-256L9S-11 2... | 256 GB | 1       | 900   | 0     | 2.47   |
| Corsair   | Force 3 SSD        | 64 GB  | 4       | 894   | 0     | 2.45   |
| OCZ       | VERTEX3            | 90 GB  | 1       | 2678  | 2     | 2.45   |
| Crucial   | CT250MX200SSD3     | 250 GB | 2       | 892   | 0     | 2.45   |
| SanDisk   | SD8SBBU240G1122    | 240 GB | 1       | 891   | 0     | 2.44   |
| Seagate   | ST100FN0021        | 100 GB | 1       | 1781  | 1     | 2.44   |
| SuperM... | SSD                | 64 GB  | 4       | 889   | 0     | 2.44   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 5       | 887   | 0     | 2.43   |
| Kingston  | SVP180S264G        | 64 GB  | 1       | 887   | 0     | 2.43   |
| Samsung   | SSD 850 EVO        | 120 GB | 27      | 885   | 0     | 2.43   |
| HPE       | MK000240GWEZF      | 240 GB | 2       | 882   | 0     | 2.42   |
| Samsung   | SSD 840 EVO        | 250 GB | 36      | 876   | 0     | 2.40   |
| Innodisk  | DEMSR- 08GB mSA... | 8 GB   | 3       | 876   | 0     | 2.40   |
| Kingston  | SNV425S264GB       | 64 GB  | 2       | 882   | 3     | 2.40   |
| Kingston  | SH103S3120G        | 120 GB | 6       | 874   | 0     | 2.40   |
| Intel     | SSDSC2BA200G3      | 200 GB | 1       | 2622  | 2     | 2.40   |
| China     | 240GB SSD          | 240 GB | 1       | 873   | 0     | 2.39   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 11      | 871   | 0     | 2.39   |
| Plextor   | PH6-CE120          | 120 GB | 1       | 864   | 0     | 2.37   |
| OCZ       | AGILITY3           | 64 GB  | 6       | 1028  | 1     | 2.36   |
| Samsung   | SSD 840 PRO Series | 512 GB | 3       | 856   | 0     | 2.35   |
| Samsung   | SSD 850 EVO        | 500 GB | 60      | 892   | 2     | 2.34   |
| Kingston  | SUV400S37240G      | 240 GB | 10      | 910   | 1     | 2.34   |
| Kingston  | SMS200S330G        | 32 GB  | 9       | 1084  | 1     | 2.32   |
| Samsung   | SSD 850 PRO        | 512 GB | 18      | 846   | 0     | 2.32   |
| ADATA     | SSD S510           | 64 GB  | 2       | 839   | 0     | 2.30   |
| Micron    | P300-MTFDDAC100SAL | 100 GB | 2       | 1551  | 503   | 2.30   |
| Intel     | SSDSCKHB120G4      | 120 GB | 2       | 834   | 0     | 2.29   |
| Advantech | SQF-SLMM2-8G-S8C   | 8 GB   | 1       | 833   | 0     | 2.28   |
| Kingston  | SMS100S264G        | 64 GB  | 1       | 833   | 0     | 2.28   |
| Unigen    | UGBS14PH8000T1X... | 8 GB   | 1       | 833   | 0     | 2.28   |
| Samsung   | SSD 850 EVO        | 250 GB | 114     | 853   | 1     | 2.27   |
| Samsung   | SSD 840 PRO Series | 256 GB | 18      | 1221  | 69    | 2.26   |
| Toshiba   | THNSNC128GBSJ      | 128 GB | 1       | 826   | 0     | 2.26   |
| Lite-On   | LAT-256M3S         | 256 GB | 1       | 825   | 0     | 2.26   |
| Transcend | TS64GMTS400S       | 64 GB  | 3       | 824   | 0     | 2.26   |
| Intel     | SSDSC2BB480G7      | 480 GB | 3       | 940   | 1     | 2.26   |
| WDC       | WDBNCE5000PNC      | 500 GB | 4       | 822   | 0     | 2.25   |
| Goodram   | SSD                | 64 GB  | 1       | 820   | 0     | 2.25   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 2       | 816   | 0     | 2.24   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 2       | 814   | 0     | 2.23   |
| ADATA     | SP600              | 128 GB | 1       | 813   | 0     | 2.23   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 12      | 813   | 0     | 2.23   |
| Apple     | SSD SM0512F        | 500 GB | 2       | 812   | 0     | 2.23   |
| Kingston  | SUV300S37A240G     | 240 GB | 1       | 807   | 0     | 2.21   |
| Plextor   | PH6-CE120-G        | 120 GB | 1       | 804   | 0     | 2.20   |
| Crucial   | CT240M500SSD3      | 240 GB | 3       | 803   | 0     | 2.20   |
| ADATA     | SSD S599           | 40 GB  | 1       | 802   | 0     | 2.20   |
| China     | SSD                | 480 GB | 1       | 802   | 0     | 2.20   |
| SanDisk   | X300 MSATA         | 256 GB | 1       | 800   | 0     | 2.19   |
| Samsung   | SSD 850 PRO        | 256 GB | 25      | 845   | 1     | 2.18   |
| Plextor   | PX-64G5Le          | 64 GB  | 1       | 791   | 0     | 2.17   |
| SanDisk   | SSD U110           | 128 GB | 1       | 791   | 0     | 2.17   |
| Crucial   | CT960M500SSD1      | 960 GB | 2       | 787   | 0     | 2.16   |
| SanDisk   | SSD PLUS 120 GB    | 120 GB | 4       | 843   | 1     | 2.16   |
| Corsair   | Force GT           | 120 GB | 2       | 1377  | 2     | 2.16   |
| Samsung   | MZNLN128HCGR-000L1 | 128 GB | 1       | 781   | 0     | 2.14   |
| China     | SATA SSD           | 16 GB  | 67      | 778   | 0     | 2.13   |
| Goodram   | SSD                | 120 GB | 6       | 775   | 0     | 2.12   |
| Intel     | SSDSC2KG240G7      | 240 GB | 2       | 1289  | 2     | 2.12   |
| Samsung   | MZMTE128HMGR-00007 | 128 GB | 3       | 869   | 1     | 2.12   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 2       | 1119  | 165   | 2.12   |
| Kingston  | RBUSNS8180S3128GI  | 128 GB | 1       | 771   | 0     | 2.11   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 4       | 768   | 0     | 2.11   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 6       | 767   | 0     | 2.10   |
| Kingston  | SMS151S332GD1      | 32 GB  | 1       | 767   | 0     | 2.10   |
| Toshiba   | Q300               | 480 GB | 2       | 762   | 0     | 2.09   |
| OCZ       | VERTEX3            | 120 GB | 8       | 1218  | 21    | 2.09   |
| SanDisk   | SDSA6DM-016G-1006  | 16 GB  | 1       | 761   | 0     | 2.09   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 16      | 761   | 0     | 2.09   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 2       | 760   | 0     | 2.08   |
| Transcend | TSG128MTS400ISI    | 128 GB | 1       | 760   | 0     | 2.08   |
| China     | SATA SSD           | 512 GB | 1       | 757   | 0     | 2.07   |
| Apple     | SSD TS256C         | 256 GB | 1       | 752   | 0     | 2.06   |
| tigo      | SSD                | 480 GB | 1       | 750   | 0     | 2.06   |
| Innodisk  | DEMSR- 16GB mSA... | 16 GB  | 1       | 748   | 0     | 2.05   |
| Kingston  | SS050S232G         | 32 GB  | 1       | 744   | 0     | 2.04   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 2       | 743   | 0     | 2.04   |
| Samsung   | SSD RBX Series ... | 128 GB | 1       | 1484  | 1     | 2.03   |
| Samsung   | SSD 850 EVO        | 2 TB   | 1       | 742   | 0     | 2.03   |
| Phison    | SATA SSD           | 120 GB | 4       | 741   | 0     | 2.03   |
| Toshiba   | Q300               | 120 GB | 1       | 740   | 0     | 2.03   |
| Samsung   | SSD RBX Series ... | 64 GB  | 2       | 739   | 0     | 2.03   |
| Mushkin   | MKNSSDTR1TB-3DL    | 1 TB   | 1       | 734   | 0     | 2.01   |
| Samsung   | MZMPA016HMCD-000L1 | 16 GB  | 1       | 1467  | 1     | 2.01   |
| SanDisk   | SSD U100           | 24 GB  | 3       | 724   | 0     | 1.98   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 3       | 717   | 0     | 1.97   |
| Kingston  | SMS200S360G        | 64 GB  | 13      | 1108  | 6     | 1.96   |
| Samsung   | SSD 850 EVO        | 1 TB   | 16      | 962   | 1     | 1.95   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 2       | 712   | 0     | 1.95   |
| SanDisk   | SD5SB2-128G-1006E  | 128 GB | 1       | 708   | 0     | 1.94   |
| Toshiba   | TL100              | 240 GB | 1       | 707   | 0     | 1.94   |
| PNY       | CS1311 120GB SSD   | 120 GB | 4       | 794   | 1     | 1.94   |
| SanDisk   | SDSSDHP128G        | 128 GB | 2       | 706   | 0     | 1.93   |
| Kingston  | SV300S37A120G      | 120 GB | 48      | 916   | 2     | 1.93   |
| Samsung   | SSD 860 EVO        | 2 TB   | 4       | 701   | 0     | 1.92   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 2       | 700   | 0     | 1.92   |
| SanDisk   | SDSSDHII240G       | 240 GB | 2       | 700   | 0     | 1.92   |
| Intel     | SSDSC2BW120A4      | 120 GB | 11      | 696   | 0     | 1.91   |
| Kingston  | SV300S37A480G      | 480 GB | 2       | 695   | 0     | 1.91   |
| Intel     | SSDSCKHW240A4      | 240 GB | 1       | 695   | 0     | 1.90   |
| Toshiba   | THNSNC128GMLJ      | 128 GB | 1       | 692   | 0     | 1.90   |
| Intel     | SSDSC2BB150G7      | 150 GB | 6       | 780   | 1     | 1.89   |
| Toshiba   | THNSNF256GMCS      | 256 GB | 1       | 690   | 0     | 1.89   |
| KingSpec  | NT-32              | 32 GB  | 2       | 690   | 0     | 1.89   |
| Dogfish   | SSD 30G            | 32 GB  | 1       | 689   | 0     | 1.89   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 10      | 687   | 0     | 1.88   |
| Kingston  | SHFS37A120G        | 120 GB | 10      | 894   | 1     | 1.88   |
| Phison    | BP4 mSATA SSD      | 240 GB | 1       | 686   | 0     | 1.88   |
| Transcend | TS256GSSD370       | 256 GB | 1       | 683   | 0     | 1.87   |
| ADATA     | SP600              | 64 GB  | 2       | 683   | 0     | 1.87   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 2       | 680   | 0     | 1.87   |
| Corsair   | Force LE SSD       | 120 GB | 1       | 680   | 0     | 1.86   |
| SanDisk   | SD7SB7S-512G-1006  | 512 GB | 1       | 677   | 0     | 1.86   |
| Samsung   | SSD 870 QVO        | 4 TB   | 1       | 674   | 0     | 1.85   |
| Intel     | SSDSC2BW240A3F     | 240 GB | 1       | 673   | 0     | 1.85   |
| OCZ       | ARC100             | 240 GB | 3       | 673   | 0     | 1.85   |
| Transcend | TS64GSSD340        | 64 GB  | 2       | 672   | 0     | 1.84   |
| Plextor   | PX-128M7VC         | 128 GB | 1       | 671   | 0     | 1.84   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 2       | 671   | 0     | 1.84   |
| Intel     | SSDSC2BX400G4      | 400 GB | 2       | 666   | 0     | 1.83   |
| OWC       | Mercury Extreme... | 240 GB | 1       | 665   | 0     | 1.82   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 5       | 736   | 1     | 1.81   |
| Lite-On   | LCH-128V2S-HP      | 128 GB | 1       | 659   | 0     | 1.81   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 2       | 658   | 0     | 1.80   |
| Goodram   | SSDPR-CX400-128    | 128 GB | 3       | 657   | 0     | 1.80   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 6       | 853   | 1     | 1.80   |
| SanDisk   | SD6SF1M-032G-1006  | 32 GB  | 1       | 657   | 0     | 1.80   |
| SanDisk   | SSD U100           | 16 GB  | 8       | 653   | 0     | 1.79   |
| Protectli | 16GB mSATA         | 16 GB  | 2       | 650   | 0     | 1.78   |
| Kingston  | SMSM150S324G2      | 24 GB  | 1       | 650   | 0     | 1.78   |
| Samsung   | SG9MSM6D024GPM00   | 22 GB  | 1       | 649   | 0     | 1.78   |
| Smartbuy  | SSD                | 240 GB | 1       | 647   | 0     | 1.77   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 2       | 646   | 0     | 1.77   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 1       | 641   | 0     | 1.76   |
| Intel     | SSDSC2KW512G8      | 512 GB | 1       | 641   | 0     | 1.76   |
| ADATA     | IM2S3134N-064GM    | 64 GB  | 19      | 637   | 0     | 1.75   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 4       | 637   | 0     | 1.75   |
| OCZ       | VERTEX460A         | 120 GB | 2       | 634   | 0     | 1.74   |
| Kingston  | SV300S37A60G       | 64 GB  | 17      | 1047  | 49    | 1.74   |
| Corsair   | Force LS SSD       | 64 GB  | 6       | 1001  | 169   | 1.74   |
| Kingston  | SM2280S3120G       | 120 GB | 3       | 633   | 0     | 1.74   |
| Samsung   | MZNLN512HMJP-000H1 | 512 GB | 1       | 633   | 0     | 1.74   |
| Corsair   | Force GS           | 180 GB | 2       | 631   | 0     | 1.73   |
| Mach X... | MXSSD2MSLD16G-V    | 16 GB  | 1       | 629   | 0     | 1.73   |
| Samsung   | SSD 840 Series     | 500 GB | 2       | 894   | 1     | 1.72   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 4       | 625   | 0     | 1.71   |
| Kingston  | SS200S330G         | 32 GB  | 3       | 624   | 0     | 1.71   |
| SanDisk   | SDSSDP128G         | 128 GB | 10      | 624   | 0     | 1.71   |
| Kingston  | SV300S37A240G      | 240 GB | 11      | 802   | 3     | 1.71   |
| Kingston  | SUV400S37120G      | 120 GB | 18      | 655   | 53    | 1.70   |
| Kingston  | SH103S3240G        | 240 GB | 4       | 1059  | 453   | 1.69   |
| Innodisk  | Corp. mSATA 3SE... | 2 GB   | 1       | 617   | 0     | 1.69   |
| Intel     | SSDSC2CT120A3      | 120 GB | 6       | 1185  | 2     | 1.68   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 1       | 612   | 0     | 1.68   |
| Advantech | SQF-S25M4-16G-S9C  | 16 GB  | 1       | 612   | 0     | 1.68   |
| Transcend | TS128GSSD230S      | 128 GB | 3       | 611   | 0     | 1.68   |
| SanDisk   | SSD i100           | 32 GB  | 3       | 1045  | 4     | 1.67   |
| Crucial   | CT128M550SSD4      | 128 GB | 1       | 610   | 0     | 1.67   |
| Apacer    | AST220             | 120 GB | 1       | 610   | 0     | 1.67   |
| SanDisk   | SDSSDXP120G        | 120 GB | 1       | 608   | 0     | 1.67   |
| Kingston  | SUV500120G         | 120 GB | 3       | 608   | 0     | 1.67   |
| SanDisk   | SD9SB8W-256G-1006  | 256 GB | 1       | 607   | 0     | 1.66   |
| Intel     | SSDMCEAC060B3      | 64 GB  | 4       | 685   | 1     | 1.66   |
| Team      | TEAML5Lite3D1T     | 1 TB   | 1       | 601   | 0     | 1.65   |
| SanDisk   | SDSSDP064G         | 64 GB  | 9       | 607   | 1     | 1.65   |
| Goodram   | IRIDIUM PRO        | 120 GB | 1       | 599   | 0     | 1.64   |
| Crucial   | CT1050MX300SSD4    | 1 TB   | 2       | 1138  | 3     | 1.62   |
| Apacer    | AS510S             | 128 GB | 1       | 592   | 0     | 1.62   |
| KingSpec  | KSD-SA25.7-016MJ   | 16 GB  | 1       | 592   | 0     | 1.62   |
| Kingston  | HyperX Fury 3D     | 240 GB | 1       | 591   | 0     | 1.62   |
| Micron    | MTFDDAK120MBB-1... | 120 GB | 1       | 590   | 0     | 1.62   |
| SanDisk   | SDSA6GM-016G-1006  | 16 GB  | 1       | 589   | 0     | 1.62   |
| SK hynix  | SH920 mSATA        | 128 GB | 1       | 586   | 0     | 1.61   |
| Intel     | SSDSC2BB012T7      | 1.2 TB | 2       | 1169  | 1     | 1.60   |
| Kingston  | SKC300S37A240G     | 240 GB | 1       | 583   | 0     | 1.60   |
| Vaseky    | V800-32G           | 32 GB  | 1       | 582   | 0     | 1.60   |
| Crucial   | CT256MX100SSD1     | 256 GB | 9       | 579   | 0     | 1.59   |
| SanDisk   | X400 M.2 2280      | 128 GB | 7       | 579   | 0     | 1.59   |
| Advantech | SQF-SLMM2-8G-8SE   | 8 GB   | 3       | 577   | 0     | 1.58   |
| Plextor   | PX-AG256M6e        | 256 GB | 1       | 576   | 0     | 1.58   |
| Samsung   | MZ7TE128HMGR-000H1 | 128 GB | 1       | 572   | 0     | 1.57   |
| Transcend | TS128GMTS550T      | 128 GB | 1       | 572   | 0     | 1.57   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 4       | 568   | 0     | 1.56   |
| Patriot   | FLARE              | 64 GB  | 1       | 562   | 0     | 1.54   |
| Samsung   | MZNLN256HAJQ-000H1 | 256 GB | 1       | 558   | 0     | 1.53   |
| SK hynix  | SC311 SATA         | 256 GB | 8       | 556   | 0     | 1.53   |
| Samsung   | MZ7LN128HAHQ-000L2 | 128 GB | 1       | 554   | 0     | 1.52   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 4       | 553   | 0     | 1.52   |
| OWC       | Mercury Electra... | 240 GB | 3       | 552   | 0     | 1.51   |
| Indilinx  | IND-S3MP-256G      | 256 GB | 1       | 552   | 0     | 1.51   |
| Samsung   | MZ7TE512HMHP-000L2 | 512 GB | 1       | 551   | 0     | 1.51   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 2       | 550   | 0     | 1.51   |
| ADATA     | IMSS314-064GB      | 64 GB  | 1       | 549   | 0     | 1.51   |
| Kingston  | RBU-SMS151S364GG   | 64 GB  | 1       | 549   | 0     | 1.50   |
| Kingston  | SM2280S3G2240G     | 240 GB | 1       | 548   | 0     | 1.50   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 2       | 546   | 0     | 1.50   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 9       | 2165  | 7     | 1.49   |
| SPCC      | SSD                | 64 GB  | 5       | 544   | 0     | 1.49   |
| Samsung   | MZ7TD128HAFV-00000 | 128 GB | 1       | 544   | 0     | 1.49   |
| Phison    | SATA SSD           | 16 GB  | 45      | 544   | 0     | 1.49   |
| Crucial   | CT240M500SSD1      | 240 GB | 7       | 756   | 234   | 1.49   |
| SanDisk   | X400 M.2 2280      | 256 GB | 4       | 541   | 0     | 1.48   |
| OCZ       | VERTEX3            | 240 GB | 2       | 1232  | 511   | 1.48   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 3       | 540   | 0     | 1.48   |
| Seagate   | ST400FP0021        | 400 GB | 1       | 539   | 0     | 1.48   |
| Apacer    | AS220              | 64 GB  | 1       | 536   | 0     | 1.47   |
| Hoodisk   | SSD                | 16 GB  | 18      | 536   | 0     | 1.47   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 3       | 535   | 0     | 1.47   |
| Intel     | SSDSC2BW240H6      | 240 GB | 4       | 535   | 0     | 1.47   |
| SanDisk   | SDSSDHII120G       | 120 GB | 4       | 534   | 0     | 1.46   |
| SanDisk   | SSD i110           | 32 GB  | 3       | 1121  | 340   | 1.44   |
| SanDisk   | SDSSDH3500G        | 500 GB | 2       | 524   | 0     | 1.44   |
| Innodisk  | Corp. - mSATA 3IE3 | 64 GB  | 1       | 523   | 0     | 1.44   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 1       | 522   | 0     | 1.43   |
| Apple     | SSD SM256C         | 256 GB | 1       | 520   | 0     | 1.43   |
| SanDisk   | Ultra II           | 480 GB | 5       | 520   | 0     | 1.42   |
| Team      | T2535T240G         | 240 GB | 1       | 519   | 0     | 1.42   |
| Transcend | TS32GSSD340K       | 32 GB  | 2       | 518   | 0     | 1.42   |
| Corsair   | CSSD-F60GB2        | 64 GB  | 1       | 516   | 0     | 1.42   |
| China     | NGFF 2242 32GB SSD | 32 GB  | 1       | 516   | 0     | 1.42   |
| Crucial   | CT250MX200SSD4     | 250 GB | 2       | 515   | 0     | 1.41   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 5       | 513   | 0     | 1.41   |
| Phison    | SATA SSD           | 8 GB   | 1       | 508   | 0     | 1.39   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 2       | 508   | 0     | 1.39   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 1       | 508   | 0     | 1.39   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 4       | 508   | 0     | 1.39   |
| Corsair   | Force 3 SSD        | 120 GB | 6       | 934   | 169   | 1.39   |
| SanDisk   | i110 128G          | 128 GB | 1       | 504   | 0     | 1.38   |
| Toshiba   | A100               | 240 GB | 1       | 503   | 0     | 1.38   |
| V-GeN     | V-GEN08AS19FS120IT | 120 GB | 1       | 500   | 0     | 1.37   |
| Lite-On   | LCH-128V2S-11 2... | 128 GB | 2       | 500   | 0     | 1.37   |
| Protectli | 480GB mSATA        | 480 GB | 2       | 499   | 0     | 1.37   |
| Intenso   | SSD Sata III       | 120 GB | 6       | 499   | 0     | 1.37   |
| Hoodisk   | SSD                | 32 GB  | 50      | 498   | 0     | 1.37   |
| Kingston  | SMS200S3120G       | 120 GB | 14      | 1011  | 13    | 1.36   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 7       | 1779  | 581   | 1.36   |
| Toshiba   | Q300 Pro           | 128 GB | 2       | 494   | 0     | 1.35   |
| ADATA     | SU630              | 960 GB | 1       | 494   | 0     | 1.35   |
| Smartbuy  | SSD                | 120 GB | 2       | 494   | 0     | 1.35   |
| ADATA     | SP900              | 128 GB | 7       | 493   | 0     | 1.35   |
| Lenovo    | LS510-mSATA-240GB  | 240 GB | 1       | 490   | 0     | 1.34   |
| Plextor   | PX-64G7Me          | 64 GB  | 1       | 489   | 0     | 1.34   |
| SanDisk   | SD8TB8U512G1001    | 512 GB | 2       | 489   | 0     | 1.34   |
| SanDisk   | X400 2.5 7MM       | 256 GB | 1       | 489   | 0     | 1.34   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 2       | 488   | 0     | 1.34   |
| HP        | SSD M700           | 240 GB | 1       | 487   | 0     | 1.34   |
| Crucial   | CT250MX500SSD4     | 250 GB | 4       | 487   | 0     | 1.34   |
| DST       | DST8128-MSATA-1... | 128 GB | 1       | 485   | 0     | 1.33   |
| SPCC      | SSD                | 120 GB | 9       | 483   | 0     | 1.32   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 2       | 482   | 0     | 1.32   |
| Samsung   | MZYLN256HCHP-000L2 | 256 GB | 2       | 480   | 0     | 1.32   |
| Goodram   | IRP-SSDPR-S25C-256 | 256 GB | 1       | 478   | 0     | 1.31   |
| SanDisk   | SD8SB8U256G1001    | 256 GB | 1       | 473   | 0     | 1.30   |
| OCZ       | VERTEX2 3.5        | 120 GB | 1       | 472   | 0     | 1.30   |
| Samsung   | SSD 750 EVO        | 500 GB | 2       | 471   | 0     | 1.29   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 6       | 493   | 3     | 1.29   |
| Intenso   | lntenso SSD Sat... | 120 GB | 1       | 469   | 0     | 1.29   |
| Samsung   | MZ7LN128HCHP-00000 | 128 GB | 2       | 467   | 0     | 1.28   |
| SK hynix  | SC311 SATA         | 128 GB | 2       | 467   | 0     | 1.28   |
| Samsung   | MZNLN512HMJP-000L7 | 512 GB | 2       | 465   | 0     | 1.28   |
| Toshiba   | THNSFJ128GMCT      | 128 GB | 1       | 462   | 0     | 1.27   |
| Intel     | SSDSCMMW240A3L     | 240 GB | 1       | 462   | 0     | 1.27   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 2       | 460   | 0     | 1.26   |
| Intel     | SSDSC2BW180A4      | 180 GB | 10      | 459   | 0     | 1.26   |
| Intel     | SSDMCEAW120A4      | 120 GB | 4       | 458   | 0     | 1.26   |
| KingFast  | SSD                | 16 GB  | 6       | 458   | 0     | 1.26   |
| Delkin... | ME16TGPXQ-XN000-D  | 16 GB  | 1       | 916   | 1     | 1.26   |
| Seagate   | BarraCuda 120 S... | 1 TB   | 1       | 456   | 0     | 1.25   |
| SPCC      | SSD                | 1 TB   | 21      | 456   | 0     | 1.25   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 6       | 468   | 1     | 1.25   |
| SanDisk   | SDSSDA120G         | 120 GB | 30      | 461   | 25    | 1.25   |
| CWDISK    | SSD                | 32 GB  | 1       | 455   | 0     | 1.25   |
| OCZ       | VERTEX2            | 120 GB | 2       | 455   | 0     | 1.25   |
| Patriot   | Burst              | 480 GB | 2       | 455   | 0     | 1.25   |
| SanDisk   | SDSSDH2256G        | 256 GB | 1       | 454   | 0     | 1.24   |
| Apacer    | 32GB SATA Flash... | 32 GB  | 10      | 622   | 105   | 1.23   |
| SATADOM   | ML 3SE             | 64 GB  | 1       | 449   | 0     | 1.23   |
| Micron    | 5200_MTFDDAK1T9TDN | 1.9 TB | 2       | 446   | 0     | 1.22   |
| Samsung   | Portable SSD T3    | 500 GB | 1       | 446   | 0     | 1.22   |
| Intel     | SSDSC2BF180A4H     | 180 GB | 4       | 445   | 0     | 1.22   |
| Intel     | SSDSC2KW256G8      | 256 GB | 12      | 454   | 1     | 1.22   |
| AEGO      | SSD                | 120 GB | 1       | 445   | 0     | 1.22   |
| SanDisk   | SD7SB6S128G1001    | 128 GB | 1       | 444   | 0     | 1.22   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 7       | 442   | 0     | 1.21   |
| PNY       | CS900 120GB SSD    | 120 GB | 34      | 442   | 0     | 1.21   |
| Innodisk  | DEMSR- 16GB mSA... | 16 GB  | 4       | 441   | 0     | 1.21   |
| Samsung   | SSD PM830 FDE 2... | 256 GB | 1       | 440   | 0     | 1.21   |
| Phison    | SATA SSD           | 128 GB | 5       | 438   | 0     | 1.20   |
| ADATA     | SU750              | 1 TB   | 1       | 435   | 0     | 1.19   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 2       | 433   | 0     | 1.19   |
| SanDisk   | Ultra II           | 240 GB | 2       | 433   | 0     | 1.19   |
| Intel     | SSDSA2BT040G3      | 40 GB  | 1       | 432   | 0     | 1.19   |
| Samsung   | MZMPC032HBCD-000L1 | 32 GB  | 1       | 431   | 0     | 1.18   |
| Micron    | MTFDDAK256TBN-1... | 256 GB | 1       | 431   | 0     | 1.18   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 3       | 430   | 0     | 1.18   |
| Samsung   | MZNTE256HMHP-000L2 | 256 GB | 1       | 430   | 0     | 1.18   |
| Kingston  | SUV400S37480G      | 480 GB | 3       | 847   | 4     | 1.18   |
| Crucial   | CT480BX300SSD1     | 480 GB | 1       | 429   | 0     | 1.18   |
| Advantech | SQF-S25M8-64G-S8C  | 64 GB  | 1       | 428   | 0     | 1.17   |
| Vaseky    | V800-60G           | 64 GB  | 1       | 426   | 0     | 1.17   |
| Intel     | SSDSC2BB480G4      | 480 GB | 1       | 1278  | 2     | 1.17   |
| SK hynix  | SC300 M.2 2280     | 128 GB | 1       | 425   | 0     | 1.17   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 1       | 424   | 0     | 1.16   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 6       | 793   | 20    | 1.16   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 1       | 422   | 0     | 1.16   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 5       | 422   | 0     | 1.16   |
| SK hynix  | SC311 SATA         | 512 GB | 3       | 420   | 0     | 1.15   |
| SanDisk   | SDSSDH120GG25      | 120 GB | 1       | 419   | 0     | 1.15   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 2       | 419   | 0     | 1.15   |
| Samsung   | MZ7LH480HAHQ-00005 | 480 GB | 2       | 417   | 0     | 1.14   |
| KST       | V300               | 119 GB | 1       | 416   | 0     | 1.14   |
| Intel     | SSDSC2BP480G4      | 480 GB | 2       | 415   | 0     | 1.14   |
| AVEXIR    | E100 SERIES -      | 120 GB | 1       | 415   | 0     | 1.14   |
| Transcend | TS128GSSD370S      | 128 GB | 3       | 413   | 0     | 1.13   |
| OCZ       | VERTEX2 3.5        | 240 GB | 1       | 413   | 0     | 1.13   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 2       | 885   | 8     | 1.13   |
| Innodisk  | mSATA mini 3ME4    | 64 GB  | 1       | 411   | 0     | 1.13   |
| ORICO     | M200               | 128 GB | 1       | 411   | 0     | 1.13   |
| Transcend | TS120GESD240C      | 120 GB | 1       | 410   | 0     | 1.13   |
| Kingston  | SUV500MS120G       | 120 GB | 62      | 410   | 0     | 1.12   |
| Crucial   | CT2000BX500SSD1    | 2 TB   | 1       | 409   | 0     | 1.12   |
| Patriot   | Pyro SSD           | 240 GB | 1       | 409   | 0     | 1.12   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 2       | 406   | 0     | 1.11   |
| Mushkin   | MKNSSDRE500GB      | 500 GB | 1       | 406   | 0     | 1.11   |
| China     | SATA SSD           | 120 GB | 19      | 403   | 0     | 1.11   |
| SanDisk   | SDSSDH3 1T02       | 1 TB   | 2       | 402   | 0     | 1.10   |
| ADATA     | XM11               | 120 GB | 1       | 399   | 0     | 1.09   |
| Hoodisk   | SSD                | 64 GB  | 51      | 397   | 0     | 1.09   |
| Samsung   | SSD 650            | 120 GB | 2       | 397   | 0     | 1.09   |
| Samsung   | SSD 840 EVO        | 1 TB   | 5       | 396   | 0     | 1.09   |
| Apacer    | 128GB SATA Flas... | 128 GB | 3       | 396   | 0     | 1.09   |
| Intel     | SSDSC2BW120A3      | 120 GB | 2       | 991   | 508   | 1.08   |
| China     | MSATA 128GB SSD    | 128 GB | 1       | 393   | 0     | 1.08   |
| Netac     | SSD                | 64 GB  | 1       | 392   | 0     | 1.07   |
| Plextor   | PX-256M5Pro        | 256 GB | 1       | 392   | 0     | 1.07   |
| TCSUNBOW  | X3                 | 480 GB | 1       | 391   | 0     | 1.07   |
| Patriot   | Burst              | 240 GB | 8       | 391   | 0     | 1.07   |
| Samsung   | MZYLF128HCHP-000L2 | 128 GB | 2       | 391   | 0     | 1.07   |
| Samsung   | MZMTD256HAGM-000L1 | 256 GB | 1       | 391   | 0     | 1.07   |
| Hoodisk   | SSD                | 128 GB | 48      | 389   | 0     | 1.07   |
| Toshiba   | TR200              | 240 GB | 8       | 388   | 0     | 1.07   |
| Kingston  | SQ500S37480G       | 480 GB | 1       | 388   | 0     | 1.06   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 2       | 387   | 0     | 1.06   |
| SanDisk   | SD7SB2Q-512G-1006  | 512 GB | 1       | 386   | 0     | 1.06   |
| SanDisk   | SSD U100           | 128 GB | 2       | 386   | 0     | 1.06   |
| KingSpec  | P3-120             | 120 GB | 1       | 385   | 0     | 1.06   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 1       | 385   | 0     | 1.06   |
| SK hynix  | SC308 SATA         | 256 GB | 4       | 733   | 2     | 1.05   |
| SanDisk   | SDSSDA240G         | 240 GB | 23      | 419   | 4     | 1.05   |
| SanDisk   | SD9SB8W128G1122    | 128 GB | 1       | 381   | 0     | 1.05   |
| Kingston  | SHFS37A240G        | 240 GB | 7       | 381   | 0     | 1.04   |
| OCZ       | VECTOR150          | 120 GB | 1       | 758   | 1     | 1.04   |
| Patriot   | Burst              | 960 GB | 2       | 378   | 0     | 1.04   |
| Intenso   | SSD SATAIII        | 120 GB | 6       | 379   | 1     | 1.04   |
| Samsung   | Portable SSD T5    | 500 GB | 4       | 376   | 0     | 1.03   |
| Team      | T253X5480G         | 480 GB | 1       | 374   | 0     | 1.03   |
| OCZ       | TRION150           | 480 GB | 1       | 373   | 0     | 1.02   |
| China     | SATA SSD           | 128 GB | 8       | 371   | 0     | 1.02   |
| SanDisk   | SDSSDHII960G       | 960 GB | 2       | 371   | 0     | 1.02   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 1       | 369   | 0     | 1.01   |
| Samsung   | MZNTY128HDHP-00000 | 128 GB | 1       | 367   | 0     | 1.01   |
| Samsung   | MZ7KM960HAHP-0Z005 | 960 GB | 1       | 366   | 0     | 1.00   |
| OCZ       | TRION100           | 240 GB | 2       | 365   | 0     | 1.00   |
| Apacer    | APSDM050GM1AN-T... | 54 GB  | 1       | 364   | 0     | 1.00   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 2       | 364   | 0     | 1.00   |
| Samsung   | MZ7LM240HMHQ-00005 | 240 GB | 2       | 363   | 0     | 1.00   |
| KingDian  | S400               | 120 GB | 1       | 361   | 0     | 0.99   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 2       | 361   | 0     | 0.99   |
| Samsung   | MZNLN256HCHP-000H1 | 256 GB | 1       | 361   | 0     | 0.99   |
| Zheino    | CHN-mSATAM3-256    | 256 GB | 2       | 361   | 0     | 0.99   |
| TCSUNBOW  | M1                 | 32 GB  | 4       | 360   | 0     | 0.99   |
| Transcend | TS128GMTS400       | 128 GB | 2       | 360   | 0     | 0.99   |
| Crucial   | CT525MX300SSD1     | 528 GB | 15      | 568   | 2     | 0.98   |
| Samsung   | MZNTY128HDHP-000L1 | 128 GB | 1       | 358   | 0     | 0.98   |
| SanDisk   | SSD U110           | 16 GB  | 9       | 358   | 0     | 0.98   |
| Toshiba   | TR200              | 480 GB | 1       | 358   | 0     | 0.98   |
| SanDisk   | SD8TN8U256G1001    | 256 GB | 2       | 356   | 0     | 0.98   |
| SanDisk   | SDEZS25-240G-Z01   | 240 GB | 2       | 355   | 0     | 0.97   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 3       | 355   | 0     | 0.97   |
| SanDisk   | SSD PLUS           | 120 GB | 29      | 355   | 0     | 0.97   |
| China     | SATA2 32GB SSD     | 32 GB  | 1       | 354   | 0     | 0.97   |
| Samsung   | SSD 860 EVO        | 500 GB | 69      | 354   | 0     | 0.97   |
| Kingston  | SVP100S2512G       | 512 GB | 1       | 353   | 0     | 0.97   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 13      | 353   | 0     | 0.97   |
| Transcend | 3E128-TS2-550B01   | 100 GB | 4       | 502   | 257   | 0.96   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 2       | 351   | 0     | 0.96   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 5       | 351   | 0     | 0.96   |
| Lenovo    | SSD SL700 240G     | 240 GB | 1       | 350   | 0     | 0.96   |
| SanDisk   | SDSSDP256G         | 256 GB | 2       | 349   | 0     | 0.96   |
| Kingston  | SV200S3128G        | 128 GB | 1       | 1746  | 4     | 0.96   |
| Hoodisk   | SSD                | 256 GB | 10      | 348   | 0     | 0.96   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 3       | 348   | 0     | 0.96   |
| Kingston  | SA400S37960G       | 960 GB | 5       | 348   | 0     | 0.95   |
| KIOXIA... | SATA SSD           | 240 GB | 1       | 346   | 0     | 0.95   |
| Samsung   | SSD 860 PRO        | 1 TB   | 5       | 345   | 0     | 0.95   |
| SanDisk   | SD6SB1M064G1022I   | 64 GB  | 6       | 343   | 0     | 0.94   |
| ORICO     | M200               | 512 GB | 1       | 343   | 0     | 0.94   |
| Samsung   | SSD 860 EVO        | 250 GB | 58      | 342   | 0     | 0.94   |
| Crucial   | CT525MX300SSD4     | 528 GB | 2       | 370   | 2     | 0.94   |
| Apacer    | 64GB SATA Flash... | 64 GB  | 10      | 385   | 20    | 0.94   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 3       | 342   | 0     | 0.94   |
| Kingston  | RBUSNS8180DS3128GH | 128 GB | 3       | 341   | 0     | 0.94   |
| HP        | SSD S600           | 120 GB | 1       | 339   | 0     | 0.93   |
| China     | SATA SSD           | 64 GB  | 11      | 459   | 10    | 0.93   |
| Samsung   | SSD 860 QVO        | 1 TB   | 15      | 339   | 0     | 0.93   |
| Samsung   | SSD 860 EVO        | 4 TB   | 1       | 339   | 0     | 0.93   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 5       | 338   | 0     | 0.93   |
| OCZ       | TRION150           | 240 GB | 2       | 338   | 0     | 0.93   |
| Intel     | SSDSC2BW180A3H     | 180 GB | 2       | 337   | 0     | 0.92   |
| SanDisk   | SD8SN8U128G1001    | 128 GB | 1       | 335   | 0     | 0.92   |
| Samsung   | MZ7LF192HCGS-000L1 | 192 GB | 1       | 335   | 0     | 0.92   |
| SanDisk   | SD7SN3Q512G1002    | 512 GB | 2       | 335   | 0     | 0.92   |
| Lite-On   | IT LCS-256L9S      | 256 GB | 1       | 334   | 0     | 0.92   |
| SanDisk   | SD6SP1M256G1102    | 256 GB | 1       | 333   | 0     | 0.91   |
| Hoodisk   | SSD                | 512 GB | 3       | 332   | 0     | 0.91   |
| Mushkin   | MKNSSDAT120GB-V    | 120 GB | 1       | 332   | 0     | 0.91   |
| Crucial   | CT275MX300SSD4     | 275 GB | 4       | 386   | 44    | 0.91   |
| WDC       | WDS500G1R0A-68A4W0 | 500 GB | 3       | 332   | 0     | 0.91   |
| SanDisk   | SD6SB1M-032G-1006  | 32 GB  | 1       | 331   | 0     | 0.91   |
| Samsung   | SSD 860 PRO        | 256 GB | 19      | 330   | 0     | 0.91   |
| Protectli | 32GB mSATA         | 32 GB  | 7       | 326   | 0     | 0.89   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 2       | 326   | 0     | 0.89   |
| Vaseky    | V800-120G          | 120 GB | 1       | 325   | 0     | 0.89   |
| Intel     | SSDSC2KB480G8R     | 480 GB | 1       | 325   | 0     | 0.89   |
| Apacer    | 16GB SATA Flash... | 16 GB  | 19      | 471   | 13    | 0.89   |
| Pioneer   | APS-SL3N-256       | 256 GB | 2       | 322   | 0     | 0.88   |
| Kingston  | SUV500M8120G       | 120 GB | 1       | 320   | 0     | 0.88   |
| Mushkin   | MKNSSDRE250GB-LT   | 250 GB | 1       | 319   | 0     | 0.87   |
| SanDisk   | SDSSDH32000G       | 2 TB   | 1       | 319   | 0     | 0.87   |
| Faspeed   | H5-240G            | 240 GB | 1       | 318   | 0     | 0.87   |
| KingFast  | SSD                | 120 GB | 22      | 313   | 42    | 0.86   |
| Intel     | SSDSC2KB240G8      | 240 GB | 17      | 312   | 0     | 0.86   |
| Toshiba   | THNSNX032GTNT      | 32 GB  | 1       | 312   | 0     | 0.86   |
| ADATA     | SP900              | 256 GB | 2       | 614   | 212   | 0.85   |
| Kingston  | SA400S371920G      | 1.9 TB | 1       | 310   | 0     | 0.85   |
| Crucial   | CT120BX500SSD1     | 120 GB | 45      | 310   | 0     | 0.85   |
| Kingston  | SUV300S37A120G     | 120 GB | 1       | 309   | 0     | 0.85   |
| SanDisk   | X400 2.5 7MM       | 128 GB | 1       | 307   | 0     | 0.84   |
| Intel     | SSDSC2BW240A4      | 240 GB | 5       | 307   | 0     | 0.84   |
| Hyundai   | 120GB SSD          | 120 GB | 1       | 306   | 0     | 0.84   |
| Corsair   | CMFSSD-256D1       | 256 GB | 1       | 305   | 0     | 0.84   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 1       | 303   | 0     | 0.83   |
| Samsung   | MZNLN128HAHQ-000L2 | 128 GB | 1       | 302   | 0     | 0.83   |
| Phison    | SATA SSD           | 32 GB  | 7       | 301   | 0     | 0.83   |
| China     | C500               | 128 GB | 2       | 301   | 0     | 0.83   |
| Crucial   | CT500MX200SSD1     | 500 GB | 5       | 300   | 0     | 0.82   |
| Plextor   | PX-512M8VC         | 512 GB | 1       | 300   | 0     | 0.82   |
| China     | SATA SSD           | 32 GB  | 18      | 391   | 11    | 0.82   |
| Samsung   | MZMPC128HBFU-000H1 | 128 GB | 2       | 297   | 0     | 0.81   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 3       | 296   | 0     | 0.81   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 2       | 296   | 0     | 0.81   |
| Intel     | SSDSC2CT240A3      | 240 GB | 1       | 2370  | 7     | 0.81   |
| SanDisk   | SSD U110           | 24 GB  | 1       | 295   | 0     | 0.81   |
| Integral  | V Series SATA SSD  | 120 GB | 3       | 295   | 0     | 0.81   |
| MyDigi... | SB2                | 128 GB | 3       | 592   | 3     | 0.81   |
| WDC       | WDS200T2B0A        | 2 TB   | 1       | 588   | 1     | 0.81   |
| HP        | SSD S700 Pro       | 512 GB | 2       | 294   | 0     | 0.81   |
| Transcend | TS64GSSD370        | 64 GB  | 20      | 292   | 0     | 0.80   |
| Samsung   | MZHPV256HDGL-00000 | 256 GB | 1       | 292   | 0     | 0.80   |
| Kingston  | SUV500MS240G       | 240 GB | 35      | 291   | 0     | 0.80   |
| Intel     | SSDSC2CW120A3      | 120 GB | 7       | 1817  | 727   | 0.78   |
| ADATA     | SSD S511           | 64 GB  | 1       | 286   | 0     | 0.78   |
| China     | G7-240G PLUS       | 240 GB | 1       | 285   | 0     | 0.78   |
| OCZ       | AGILITY4           | 128 GB | 3       | 314   | 1     | 0.78   |
| SK hynix  | SHGS31-250GS-2     | 250 GB | 3       | 283   | 0     | 0.78   |
| Fordisk   | 64G 6.0Gb          | 64 GB  | 1       | 282   | 0     | 0.78   |
| Kingston  | SA400S37120G       | 120 GB | 91      | 298   | 2     | 0.77   |
| Smart     | SSD XceedValue2... | 32 GB  | 1       | 280   | 0     | 0.77   |
| China     | M10C               | 256 GB | 2       | 280   | 0     | 0.77   |
| OCZ       | ARC100             | 120 GB | 1       | 279   | 0     | 0.77   |
| SanDisk   | SD9SN8W128G1002    | 128 GB | 1       | 278   | 0     | 0.76   |
| Transcend | TS32GMTS400S       | 32 GB  | 3       | 278   | 0     | 0.76   |
| SK hynix  | SC401 SATA         | 512 GB | 1       | 278   | 0     | 0.76   |
| SanDisk   | SDSA6MM-008G-1006  | 8 GB   | 4       | 276   | 0     | 0.76   |
| ADATA     | SU650              | 960 GB | 2       | 358   | 145   | 0.76   |
| Ramsta    | SSD S800           | 120 GB | 1       | 275   | 0     | 0.75   |
| Apacer    | AS350              | 120 GB | 1       | 274   | 0     | 0.75   |
| Kingston  | SKC400S37256G      | 256 GB | 1       | 271   | 0     | 0.74   |
| Crucial   | CT250MX500SSD1     | 250 GB | 59      | 270   | 0     | 0.74   |
| Intel     | SSDSC2BB120G4C     | 120 GB | 2       | 270   | 0     | 0.74   |
| Intel     | SSDMAEXC024G3H     | 24 GB  | 1       | 269   | 0     | 0.74   |
| Team      | T253A3512G         | 512 GB | 1       | 268   | 0     | 0.74   |
| SanDisk   | SD6SB2M512G1022I   | 512 GB | 1       | 536   | 1     | 0.74   |
| Crucial   | CT500MX500SSD4     | 500 GB | 8       | 267   | 0     | 0.73   |
| Patriot   | Burst Elite        | 240 GB | 1       | 266   | 0     | 0.73   |
| SK hynix  | HFS128G32MND-2200A | 128 GB | 1       | 798   | 2     | 0.73   |
| KingSpec  | P4-120             | 120 GB | 3       | 265   | 0     | 0.73   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 1       | 264   | 0     | 0.72   |
| HP        | SSD S700           | 250 GB | 5       | 264   | 0     | 0.72   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 4       | 1121  | 22    | 0.72   |
| Samsung   | MZNLN128HCGR-000H1 | 128 GB | 1       | 263   | 0     | 0.72   |
| SanDisk   | X400 M.2 2280      | 512 GB | 2       | 263   | 0     | 0.72   |
| WDC       | WDBNCE2500PNC      | 250 GB | 3       | 263   | 0     | 0.72   |
| HP        | SSD S700 Pro       | 256 GB | 1       | 262   | 0     | 0.72   |
| Transcend | TS120GMTS420S      | 120 GB | 15      | 262   | 0     | 0.72   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 21      | 261   | 0     | 0.72   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 8       | 260   | 0     | 0.71   |
| China     | SK600-32GB         | 32 GB  | 1       | 259   | 0     | 0.71   |
| Dogfish   | SSD                | 240 GB | 1       | 259   | 0     | 0.71   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 38      | 299   | 25    | 0.71   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 17      | 265   | 1     | 0.71   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 31      | 310   | 1     | 0.71   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 2       | 256   | 0     | 0.70   |
| Crucial   | CT275MX300SSD1     | 275 GB | 12      | 579   | 351   | 0.70   |
| Intel     | SSDSA2CW300G3      | 304 GB | 1       | 256   | 0     | 0.70   |
| Samsung   | MZNLN128HAHQ-000H1 | 128 GB | 2       | 255   | 0     | 0.70   |
| ASENNO    | ASN8               | 240 GB | 1       | 254   | 0     | 0.70   |
| KingDian  | S280               | 240 GB | 2       | 253   | 0     | 0.69   |
| Intel     | SSDSA2M120G2GC     | 120 GB | 1       | 1266  | 4     | 0.69   |
| Gigaby... | GP-GSTFS31256GTND  | 256 GB | 2       | 252   | 0     | 0.69   |
| Apple     | SSD SM0512G        | 500 GB | 3       | 252   | 0     | 0.69   |
| Team      | TM8PS7512G         | 512 GB | 3       | 252   | 0     | 0.69   |
| XrayDisk  | SSD                | 64 GB  | 1       | 251   | 0     | 0.69   |
| Samsung   | MZMTE128HMGR-00000 | 128 GB | 1       | 251   | 0     | 0.69   |
| Apple     | SSD SM1024G        | 1 TB   | 1       | 251   | 0     | 0.69   |
| Samsung   | SSD 860 EVO        | 1 TB   | 43      | 250   | 1     | 0.68   |
| ADATA     | SU650              | 480 GB | 3       | 248   | 0     | 0.68   |
| Intel     | SSDSC2BA100G3C     | 100 GB | 2       | 247   | 0     | 0.68   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 1       | 247   | 0     | 0.68   |
| Intel     | SSDMAESC020G2      | 20 GB  | 1       | 246   | 0     | 0.68   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 3       | 246   | 0     | 0.67   |
| Kston     | SSD                | 32 GB  | 5       | 245   | 0     | 0.67   |
| SanDisk   | SD5SE2256G1002E    | 256 GB | 3       | 290   | 1     | 0.67   |
| Intenso   | JAJMS600M128G      | 128 GB | 1       | 245   | 0     | 0.67   |
| WDC       | WDS500G2B0A        | 500 GB | 8       | 245   | 0     | 0.67   |
| Plextor   | PX-128M5S          | 128 GB | 1       | 1216  | 4     | 0.67   |
| Seagate   | ZA240NM10001       | 240 GB | 1       | 243   | 0     | 0.67   |
| Samsung   | MZNTE256HMHP-000H1 | 256 GB | 1       | 242   | 0     | 0.66   |
| MAXIMUS   | SSD                | 128 GB | 1       | 242   | 0     | 0.66   |
| Lexar     | SSD                | 120 GB | 1       | 242   | 0     | 0.66   |
| KingDian  | S280-240GB         | 240 GB | 1       | 241   | 0     | 0.66   |
| Crucial   | CT120M500SSD1      | 120 GB | 5       | 739   | 4     | 0.66   |
| SanDisk   | SD9TB8W512G1001    | 512 GB | 2       | 239   | 0     | 0.66   |
| Samsung   | SSD 860 PRO        | 512 GB | 11      | 237   | 0     | 0.65   |
| Samsung   | MZ7LN256HMJP-000L7 | 256 GB | 1       | 236   | 0     | 0.65   |
| Micron    | MTFDDAT064MAM-1J2  | 64 GB  | 2       | 235   | 0     | 0.65   |
| Ramaxel   | RTNTE256PCA8EADL   | 256 GB | 1       | 235   | 0     | 0.65   |
| ADATA     | SU655              | 120 GB | 2       | 235   | 0     | 0.65   |
| China     | BK-64GB MSATA SSD  | 64 GB  | 1       | 234   | 0     | 0.64   |
| Seagate   | BarraCuda 120 S... | 500 GB | 2       | 233   | 0     | 0.64   |
| Kston     | SSD                | 128 GB | 9       | 257   | 1     | 0.63   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 1       | 231   | 0     | 0.63   |
| KingFast  | SSD                | 128 GB | 1       | 230   | 0     | 0.63   |
| Plextor   | PX-256M8VG         | 256 GB | 1       | 230   | 0     | 0.63   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 7       | 299   | 1     | 0.63   |
| Gigaby... | GP-GSTFS31240GNTD  | 240 GB | 2       | 230   | 0     | 0.63   |
| Kingston  | SMSM150S3128G      | 128 GB | 1       | 229   | 0     | 0.63   |
| China     | DHMSR64GD81BC1QC   | 54 GB  | 2       | 228   | 0     | 0.63   |
| Crucial   | CT500MX500SSD1     | 500 GB | 55      | 233   | 1     | 0.62   |
| ADATA     | SU650              | 120 GB | 31      | 291   | 44    | 0.62   |
| Dogfish   | SSD                | 480 GB | 1       | 680   | 2     | 0.62   |
| KingSpec  | MT-64              | 64 GB  | 2       | 225   | 0     | 0.62   |
| Transcend | TS128GMTS400S      | 128 GB | 3       | 225   | 0     | 0.62   |
| Micron    | C400-MTFDDAK064MAM | 64 GB  | 1       | 225   | 0     | 0.62   |
| Transcend | TS120GSSD220S      | 120 GB | 3       | 224   | 0     | 0.62   |
| Smartbuy  | SSD                | 256 GB | 1       | 224   | 0     | 0.61   |
| Plextor   | PX-128M5Pro        | 128 GB | 1       | 224   | 0     | 0.61   |
| WDC       | WDS100T1R0A-68A4W0 | 1 TB   | 1       | 223   | 0     | 0.61   |
| SanDisk   | SD8SBAT256G1122    | 256 GB | 1       | 223   | 0     | 0.61   |
| Samsung   | MZHPV512HDGL-000L1 | 512 GB | 1       | 222   | 0     | 0.61   |
| Corsair   | CSSD-V64GB2        | 64 GB  | 1       | 221   | 0     | 0.61   |
| BR        | SSD                | 128 GB | 1       | 221   | 0     | 0.61   |
| Seagate   | FireCuda 120 SS... | 500 GB | 1       | 221   | 0     | 0.61   |
| Transcend | TS256GSSD452K2     | 256 GB | 4       | 221   | 0     | 0.61   |
| Kingston  | SA400S37480G       | 480 GB | 30      | 224   | 1     | 0.60   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 13      | 220   | 0     | 0.60   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 6       | 1173  | 9     | 0.60   |
| Samsung   | MZ7TY128HDHP-00000 | 128 GB | 1       | 218   | 0     | 0.60   |
| Intel     | SSDSA2M160G2GN     | 160 GB | 1       | 3720  | 16    | 0.60   |
| Transcend | TS16GMTS400        | 16 GB  | 1       | 217   | 0     | 0.60   |
| Kingston  | SHSS37A240G        | 240 GB | 2       | 217   | 0     | 0.60   |
| Corsair   | Force LS SSD       | 120 GB | 3       | 260   | 336   | 0.60   |
| PNY       | CS900 240GB SSD    | 240 GB | 19      | 217   | 0     | 0.60   |
| SanDisk   | SSD PLUS           | 1 TB   | 7       | 217   | 0     | 0.60   |
| SPCC      | M.2 SSD            | 128 GB | 3       | 217   | 0     | 0.60   |
| Samsung   | MZNTY256HDHP-000L7 | 256 GB | 1       | 216   | 0     | 0.59   |
| WDC       | WDS500G2B0B-00YS70 | 500 GB | 7       | 216   | 0     | 0.59   |
| SPCC      | SSD                | 240 GB | 2       | 216   | 0     | 0.59   |
| Innodisk  | Corp. - mSATA 3ME3 | 32 GB  | 3       | 215   | 0     | 0.59   |
| TEXTORM   | B5                 | 120 GB | 1       | 214   | 0     | 0.59   |
| Kingston  | SA400S37240G       | 240 GB | 131     | 216   | 1     | 0.59   |
| SK hynix  | HFS256G39TND-N210A | 256 GB | 4       | 214   | 0     | 0.59   |
| Plextor   | PX-128S3C          | 128 GB | 1       | 213   | 0     | 0.58   |
| Transcend | TS512GSSD370       | 512 GB | 2       | 212   | 0     | 0.58   |
| Samsung   | MZMPC032HBCD-000H1 | 32 GB  | 2       | 211   | 0     | 0.58   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 2       | 211   | 0     | 0.58   |
| Lite-On   | IT LCS-128L9S-HP   | 128 GB | 2       | 211   | 0     | 0.58   |
| SanDisk   | SSD PLUS           | 240 GB | 24      | 255   | 3     | 0.58   |
| BR        | SSD                | 64 GB  | 1       | 211   | 0     | 0.58   |
| OWC       | Mercury Electra... | 1 TB   | 6       | 210   | 0     | 0.58   |
| SanDisk   | SD5SG2128G1052E    | 128 GB | 2       | 222   | 1     | 0.58   |
| Apacer    | AS340              | 240 GB | 5       | 209   | 0     | 0.57   |
| SanDisk   | SDSSDH3512G        | 512 GB | 2       | 209   | 0     | 0.57   |
| China     | OEMSSD240GB        | 240 GB | 1       | 209   | 0     | 0.57   |
| WDC       | WDS100T1R0B-68A4Z0 | 1 TB   | 1       | 209   | 0     | 0.57   |
| FORESEE   | 32GB SSD           | 32 GB  | 4       | 209   | 0     | 0.57   |
| Wicgtyp   | M900-128           | 128 GB | 2       | 207   | 0     | 0.57   |
| OCZ       | VERTEX4            | 64 GB  | 1       | 206   | 0     | 0.57   |
| Kingston  | SUV500240G         | 240 GB | 3       | 205   | 0     | 0.56   |
| SanDisk   | SD8TN8U512G1001    | 512 GB | 1       | 204   | 0     | 0.56   |
| Seagate   | FireCuda 120 SS... | 1 TB   | 2       | 204   | 0     | 0.56   |
| ADATA     | SU800              | 256 GB | 10      | 207   | 201   | 0.56   |
| ADATA     | SU800NS38          | 256 GB | 2       | 204   | 0     | 0.56   |
| Corsair   | Neutron SSD        | 128 GB | 1       | 202   | 0     | 0.55   |
| Intel     | SSDSC2BF240A4H     | 240 GB | 1       | 201   | 0     | 0.55   |
| minisf... | SSD                | 128 GB | 4       | 201   | 0     | 0.55   |
| JWX       | MSATA              | 128 GB | 1       | 200   | 0     | 0.55   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 1       | 200   | 0     | 0.55   |
| Samsung   | MZNLF128HCHP-000L1 | 128 GB | 1       | 200   | 0     | 0.55   |
| China     | 40GB SATA Flash... | 40 GB  | 1       | 200   | 0     | 0.55   |
| China     | PSX-NGFF256G       | 256 GB | 1       | 199   | 0     | 0.55   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 15      | 199   | 0     | 0.55   |
| HP        | SSD S700           | 1 TB   | 1       | 198   | 0     | 0.54   |
| Patriot   | Burst              | 120 GB | 13      | 197   | 0     | 0.54   |
| SanDisk   | X600 M.2 2280 SATA | 128 GB | 1       | 196   | 0     | 0.54   |
| Kingston  | SUV500M8240G       | 240 GB | 3       | 196   | 0     | 0.54   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 5       | 195   | 0     | 0.54   |
| Intel     | SSDSC2BW480A4      | 480 GB | 1       | 976   | 4     | 0.53   |
| Samsung   | SSD 860 QVO        | 4 TB   | 2       | 194   | 0     | 0.53   |
| Intel     | SSDMCEAW240A4      | 240 GB | 1       | 973   | 4     | 0.53   |
| Phison    | SATA SSD           | 256 GB | 1       | 194   | 0     | 0.53   |
| WDC       | PC SA530 SDASN8... | 256 GB | 1       | 194   | 0     | 0.53   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 8       | 191   | 0     | 0.53   |
| Samsung   | MZMTD128HAFV-000   | 128 GB | 1       | 191   | 0     | 0.53   |
| Advantech | SQF-S25M8-128G-ABT | 128 GB | 1       | 189   | 0     | 0.52   |
| China     | SATA3 64GB SSD     | 64 GB  | 2       | 189   | 0     | 0.52   |
| Pioneer   | APS-SL3N-128       | 128 GB | 1       | 189   | 0     | 0.52   |
| Intel     | SSDSC2KG240G8      | 240 GB | 9       | 188   | 0     | 0.52   |
| Toshiba   | Q300               | 240 GB | 2       | 188   | 0     | 0.52   |
| Crucial   | CT750MX300SSD1     | 752 GB | 1       | 187   | 0     | 0.51   |
| Innodisk  | Corp. DRPS-16GJ... | 16 GB  | 1       | 187   | 0     | 0.51   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 32      | 201   | 2     | 0.51   |
| MyDigi... | SC2 M2 SSD         | 120 GB | 1       | 186   | 0     | 0.51   |
| KimMiDi   | T900 SSD           | 128 GB | 1       | 186   | 0     | 0.51   |
| SATADOM   | SL 3IE3 V2         | 64 GB  | 7       | 185   | 0     | 0.51   |
| Intenso   | SSD                | 128 GB | 16      | 184   | 0     | 0.51   |
| Plextor   | PX-256M8VC         | 256 GB | 1       | 184   | 0     | 0.51   |
| OCZ       | VERTEX3            | 128 GB | 1       | 184   | 0     | 0.50   |
| Silico... | AAR240GS112620030  | 240 GB | 1       | 184   | 0     | 0.50   |
| Goodram   | SSDPR-CL100-120-G2 | 120 GB | 2       | 183   | 0     | 0.50   |
| Team      | T253X2256G         | 256 GB | 1       | 183   | 0     | 0.50   |
| SanDisk   | SD8SN8U-128G-1006  | 128 GB | 4       | 183   | 0     | 0.50   |
| SanDisk   | pSSD               | 32 GB  | 7       | 182   | 0     | 0.50   |
| Intel     | SSDSC2CT240A4      | 240 GB | 1       | 182   | 0     | 0.50   |
| China     | SSD 128G           | 128 GB | 1       | 181   | 0     | 0.50   |
| Samsung   | MZ7LH1T9HMLT0D3    | 1.9 TB | 2       | 180   | 0     | 0.50   |
| Dogfish   | SSD                | 512 GB | 5       | 180   | 0     | 0.49   |
| ADATA     | SU630              | 240 GB | 16      | 203   | 2     | 0.49   |
| China     | SSD                | 64 GB  | 5       | 179   | 0     | 0.49   |
| Intel     | SSDSA2SH064G1GC    | 64 GB  | 1       | 179   | 0     | 0.49   |
| Transcend | TS64GMTS400SD      | 64 GB  | 8       | 178   | 0     | 0.49   |
| ADATA     | SU800              | 1 TB   | 3       | 318   | 15    | 0.49   |
| Gigastone | Prime Series       | 128 GB | 1       | 178   | 0     | 0.49   |
| Micron    | MTFDBAK128MAG-1G1  | 128 GB | 1       | 178   | 0     | 0.49   |
| Innodisk  | DEMSR- 08GB mSA... | 8 GB   | 13      | 177   | 0     | 0.49   |
| China     | mSATA-64GB SSD     | 64 GB  | 1       | 177   | 0     | 0.49   |
| Smartbuy  | SSD                | 64 GB  | 2       | 176   | 0     | 0.48   |
| Crucial   | CT240BX500SSD1     | 240 GB | 56      | 176   | 0     | 0.48   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 3       | 176   | 0     | 0.48   |
| Pccooler  | MSATA 128G         | 128 GB | 2       | 176   | 0     | 0.48   |
| Toshiba   | THNSNJ256GCSY      | 256 GB | 2       | 175   | 0     | 0.48   |
| Toshiba   | KSG60ZMV256G M.... | 256 GB | 6       | 204   | 17    | 0.48   |
| SanDisk   | WD easystore       | 240 GB | 5       | 175   | 0     | 0.48   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 4       | 174   | 0     | 0.48   |
| Goodram   | IRP_SSDPR_S25B_480 | 480 GB | 1       | 174   | 0     | 0.48   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 1       | 174   | 0     | 0.48   |
| Crucial   | CT480BX500SSD1     | 480 GB | 17      | 181   | 1     | 0.47   |
| PNY       | CS900 250GB SSD    | 250 GB | 6       | 172   | 0     | 0.47   |
| China     | XJH-128GB          | 128 GB | 7       | 171   | 0     | 0.47   |
| Samsung   | MZMPC256HBGJ-00000 | 256 GB | 1       | 171   | 0     | 0.47   |
| PNY       | SSD2SC240G1CS27... | 240 GB | 1       | 171   | 0     | 0.47   |
| Kingston  | SUV500MS480G       | 480 GB | 12      | 173   | 1     | 0.47   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 2       | 169   | 0     | 0.46   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 2       | 169   | 0     | 0.46   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 3       | 201   | 74    | 0.46   |
| Kingston  | SMS200S3240G       | 240 GB | 1       | 168   | 0     | 0.46   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 1       | 167   | 0     | 0.46   |
| OCZ       | AGILITY3           | 240 GB | 2       | 893   | 7     | 0.45   |
| SanDisk   | SDSSDH3 500G       | 500 GB | 4       | 165   | 0     | 0.45   |
| SanDisk   | SDSSDH3 512G       | 512 GB | 3       | 163   | 0     | 0.45   |
| SK hynix  | SHGS31-500GS-2     | 500 GB | 3       | 162   | 0     | 0.45   |
| Transcend | TS128GMSA230S      | 128 GB | 42      | 162   | 0     | 0.44   |
| Samsung   | MZNLN256HMHQ-000H1 | 256 GB | 1       | 161   | 0     | 0.44   |
| EMTEC     | X150               | 240 GB | 1       | 161   | 0     | 0.44   |
| VICK      | SSD 256G           | 256 GB | 2       | 161   | 0     | 0.44   |
| Vaseky    | 128GV800           | 128 GB | 1       | 161   | 0     | 0.44   |
| Apple     | SSD SD0128F        | 121 GB | 3       | 269   | 1     | 0.44   |
| WDC       | WDS500G1R0B-68A4Z0 | 500 GB | 2       | 160   | 0     | 0.44   |
| WDC       | SSC-D0064SC-2100   | 64 GB  | 1       | 159   | 0     | 0.44   |
| Micron    | C400-MTFDDAT064MAM | 64 GB  | 3       | 851   | 343   | 0.44   |
| Kingston  | SQ500S37240G       | 240 GB | 1       | 159   | 0     | 0.44   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 2       | 159   | 0     | 0.44   |
| Samsung   | SSD PM871b M.2 ... | 256 GB | 1       | 158   | 0     | 0.43   |
| SanDisk   | SD6SB1M064G        | 64 GB  | 1       | 157   | 0     | 0.43   |
| Transcend | TS240GMTS420S      | 240 GB | 6       | 157   | 0     | 0.43   |
| Lite-On   | CV3-CE128-HP       | 128 GB | 1       | 157   | 0     | 0.43   |
| Samsung   | SSD 860 QVO        | 2 TB   | 3       | 157   | 0     | 0.43   |
| Lite-On   | LCH-128V2S         | 128 GB | 3       | 156   | 0     | 0.43   |
| Plextor   | PX-64M5M           | 64 GB  | 1       | 154   | 0     | 0.42   |
| Innodisk  | DEM24-16GM41BC1... | 16 GB  | 1       | 153   | 0     | 0.42   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 1       | 153   | 0     | 0.42   |
| Samsung   | MMCQE28GFMUP-MVA   | 128 GB | 1       | 153   | 0     | 0.42   |
| SanDisk   | SSD i110           | 16 GB  | 1       | 152   | 0     | 0.42   |
| PNY       | CS1311 480GB SSD   | 480 GB | 1       | 152   | 0     | 0.42   |
| Innodisk  | DEMSR-64GM41BC1... | 64 GB  | 1       | 152   | 0     | 0.42   |
| UDinfo    | M2S-80UB160GB-W... | 160 GB | 1       | 150   | 0     | 0.41   |
| Kingston  | SNV325S2           | 128 GB | 1       | 150   | 0     | 0.41   |
| Dogfish   | SSD                | 64 GB  | 7       | 150   | 0     | 0.41   |
| China     | SSD                | 240 GB | 4       | 149   | 0     | 0.41   |
| Transcend | TS64GSSD370S       | 64 GB  | 6       | 149   | 0     | 0.41   |
| Intenso   | IONN SSD           | 256 GB | 3       | 149   | 0     | 0.41   |
| Dogfish   | SSD                | 128 GB | 16      | 168   | 1     | 0.41   |
| ATP       | SATA III mSATA     | 120 GB | 5       | 148   | 0     | 0.41   |
| KingSpec  | NT-128             | 128 GB | 3       | 148   | 0     | 0.41   |
| Kingston  | SVP200S37A120G     | 120 GB | 1       | 741   | 4     | 0.41   |
| Protectli | 960GB mSATA        | 960 GB | 2       | 147   | 0     | 0.40   |
| Verbatim  | Vi550 S3 SSD       | 512 GB | 7       | 146   | 0     | 0.40   |
| BAITITON  | BT58SSD07M         | 120 GB | 1       | 145   | 0     | 0.40   |
| SPCC      | SPCCSolidStateDisk | 256 GB | 3       | 144   | 0     | 0.40   |
| Intel     | SSDSC2MH120A2      | 120 GB | 3       | 144   | 0     | 0.40   |
| Lite-On   | CV8-8E256-11 SATA  | 256 GB | 1       | 143   | 0     | 0.39   |
| China     | 256GB QLC SATA SSD | 256 GB | 3       | 143   | 0     | 0.39   |
| KUIJIA    | DK500-64G          | 64 GB  | 1       | 143   | 0     | 0.39   |
| Kingch... | SSD                | 64 GB  | 1       | 429   | 2     | 0.39   |
| ADATA     | SU800              | 128 GB | 10      | 162   | 1     | 0.39   |
| China     | BK-32GB MSATA SSD  | 32 GB  | 1       | 141   | 0     | 0.39   |
| Team      | TEAML5Lite3D120G   | 120 GB | 2       | 141   | 0     | 0.39   |
| Protectli | 64GB mSATA         | 64 GB  | 7       | 141   | 0     | 0.39   |
| Gigabyte  | GP-GSTFS31256GTND  | 256 GB | 1       | 141   | 0     | 0.39   |
| KingSpec  | Q-720              | 720 GB | 2       | 140   | 0     | 0.38   |
| Intenso   | SSD Sata III       | 250 GB | 2       | 138   | 0     | 0.38   |
| China     | SATA SSD           | 480 GB | 1       | 137   | 0     | 0.38   |
| China     | GM128              | 128 GB | 1       | 137   | 0     | 0.38   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 2       | 137   | 0     | 0.38   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 5       | 137   | 0     | 0.38   |
| China     | SATA3 120GB SSD    | 120 GB | 1       | 136   | 0     | 0.37   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 2       | 270   | 1     | 0.37   |
| Plextor   | PX-256M5M          | 256 GB | 1       | 135   | 0     | 0.37   |
| Intel     | SSDSC2KW128G8      | 128 GB | 3       | 134   | 0     | 0.37   |
| Samsung   | MZNTE128HMGR-000SO | 128 GB | 2       | 287   | 3     | 0.37   |
| Silico... | SP128GISSD301SV0   | 128 GB | 1       | 133   | 0     | 0.37   |
| BIWIN     | SSD                | 128 GB | 26      | 168   | 10    | 0.36   |
| ADATA     | SU650              | 240 GB | 14      | 132   | 0     | 0.36   |
| China     | SATA SSD           | 1 TB   | 1       | 131   | 0     | 0.36   |
| Samsung   | MZHPV256HDGL-000L1 | 256 GB | 1       | 131   | 0     | 0.36   |
| Micron    | MTFDDAK512TDL-1... | 512 GB | 1       | 131   | 0     | 0.36   |
| Samsung   | MZ7PD256HCGM-000H7 | 256 GB | 1       | 130   | 0     | 0.36   |
| Lite-On   | CV8-8E256          | 256 GB | 1       | 130   | 0     | 0.36   |
| Micron    | MTFDDAK256MAM-1K12 | 256 GB | 3       | 146   | 337   | 0.35   |
| Marvell   | SATAIII            | 16 GB  | 1       | 1410  | 10    | 0.35   |
| Apple     | SSD TS128E         | 121 GB | 1       | 128   | 0     | 0.35   |
| China     | SSD                | 64 GB  | 1       | 127   | 0     | 0.35   |
| Crucial   | CT960BX500SSD1     | 960 GB | 2       | 127   | 0     | 0.35   |
| Samsung   | MZNLN256HMHQ-000H7 | 256 GB | 1       | 126   | 0     | 0.35   |
| Protectli | 120GB mSATA        | 120 GB | 21      | 126   | 0     | 0.35   |
| KingSpec  | ACSC2M064mSA       | 64 GB  | 1       | 125   | 0     | 0.34   |
| China     | SATA SSD           | 240 GB | 8       | 125   | 0     | 0.34   |
| China     | 120GB SATA Flas... | 120 GB | 1       | 124   | 0     | 0.34   |
| Apacer    | AS450              | 240 GB | 1       | 123   | 0     | 0.34   |
| ZTC       | SM201-064G         | 64 GB  | 2       | 640   | 14    | 0.34   |
| Lite-On   | LCS-128M6S-HP      | 128 GB | 1       | 123   | 0     | 0.34   |
| HPE       | MK000480GWUGF      | 480 GB | 1       | 369   | 2     | 0.34   |
| ADATA     | SU750              | 256 GB | 2       | 122   | 0     | 0.34   |
| China     | SH00M120GB         | 120 GB | 2       | 122   | 0     | 0.34   |
| Inland    | SATA SSD           | 128 GB | 1       | 121   | 0     | 0.33   |
| SanDisk   | SSD PLUS           | 480 GB | 6       | 154   | 1     | 0.33   |
| SanDisk   | SD7SN3Q128G1002    | 128 GB | 2       | 120   | 0     | 0.33   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 4       | 119   | 0     | 0.33   |
| SK hynix  | HFS128G32TNF-N3A0A | 128 GB | 2       | 119   | 0     | 0.33   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 1       | 119   | 0     | 0.33   |
| Leven     | JAJS600M256C       | 256 GB | 2       | 118   | 0     | 0.33   |
| FORESEE   | 128GB SSD          | 128 GB | 44      | 118   | 0     | 0.33   |
| Intel     | SSDSC2BF240A5L     | 240 GB | 2       | 118   | 0     | 0.32   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 1       | 118   | 0     | 0.32   |
| ADATA     | SU810NS38 SATA ... | 256 GB | 1       | 117   | 0     | 0.32   |
| SanDisk   | SSD i100           | 24 GB  | 1       | 117   | 0     | 0.32   |
| Kingston  | SA400M8240G        | 240 GB | 14      | 116   | 0     | 0.32   |
| Dogfish   | SSD                | 256 GB | 11      | 116   | 0     | 0.32   |
| Intel     | SSDSCKJW180H6      | 180 GB | 1       | 115   | 0     | 0.32   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 3       | 115   | 0     | 0.32   |
| Verbatim  | Vi500 S3 480GB SSD | 480 GB | 1       | 115   | 0     | 0.32   |
| Crucial   | CT128M550SSD3      | 128 GB | 1       | 1959  | 16    | 0.32   |
| Toshiba   | THNSNC064GBSJ      | 64 GB  | 1       | 115   | 0     | 0.32   |
| Kingston  | SQ500S37120G       | 120 GB | 5       | 114   | 0     | 0.32   |
| SanDisk   | SD9SN8W512G        | 512 GB | 1       | 114   | 0     | 0.31   |
| ADATA     | SU700              | 240 GB | 1       | 114   | 0     | 0.31   |
| LDLC      | SSD                | 120 GB | 1       | 113   | 0     | 0.31   |
| Team      | T253X2512G         | 512 GB | 1       | 113   | 0     | 0.31   |
| Lite-On   | LSS-24L6G          | 24 GB  | 1       | 112   | 0     | 0.31   |
| SPCC      | SSD                | 512 GB | 9       | 112   | 0     | 0.31   |
| Crucial   | CT120BX300SSD1     | 120 GB | 3       | 112   | 0     | 0.31   |
| China     | SATA SSD           | 256 GB | 6       | 112   | 0     | 0.31   |
| Lite-On   | LCS-128L9S-11 2... | 128 GB | 2       | 112   | 0     | 0.31   |
| Lite-On   | CV8-8E128-HP       | 128 GB | 3       | 124   | 672   | 0.31   |
| SPCC      | SSD                | 128 GB | 24      | 117   | 1     | 0.31   |
| Apacer    | AS330              | 240 GB | 1       | 1006  | 8     | 0.31   |
| BIWIN     | SSD                | 256 GB | 3       | 110   | 0     | 0.30   |
| Leven     | JAJS300M240C       | 240 GB | 2       | 109   | 0     | 0.30   |
| Transcend | TS32ASTME0000A     | 32 GB  | 1       | 109   | 0     | 0.30   |
| China     | Kston128GB         | 128 GB | 1       | 109   | 0     | 0.30   |
| Mushkin   | MKNSSDRE1TB        | 1 TB   | 2       | 109   | 0     | 0.30   |
| Intel     | SSDMAEMC040G2      | 40 GB  | 1       | 217   | 1     | 0.30   |
| AMD       | R5SL240G           | 240 GB | 3       | 150   | 7     | 0.30   |
| China     | OSSD256GBTSS2      | 256 GB | 1       | 107   | 0     | 0.30   |
| Transcend | TS128GMTS830S      | 128 GB | 1       | 107   | 0     | 0.30   |
| XUNZHE    | MSATA              | 128 GB | 1       | 106   | 0     | 0.29   |
| Intel     | SSDSC2KF128G8 SATA | 128 GB | 1       | 106   | 0     | 0.29   |
| China     | BR                 | 64 GB  | 1       | 106   | 0     | 0.29   |
| SK hynix  | SC401 SATA         | 256 GB | 1       | 106   | 0     | 0.29   |
| Intel     | SSDSC2KG480G8R     | 480 GB | 2       | 105   | 0     | 0.29   |
| Phison    | SATA SSD           | 1 TB   | 1       | 105   | 0     | 0.29   |
| Star D... | SATA SSD           | 960 GB | 1       | 105   | 0     | 0.29   |
| Apacer    | AS350              | 256 GB | 4       | 104   | 0     | 0.29   |
| China     | CF120GB            | 120 GB | 1       | 104   | 0     | 0.29   |
| Transcend | TS128GMTS430S      | 128 GB | 8       | 103   | 0     | 0.28   |
| Transcend | TS240GSSD220S      | 240 GB | 2       | 103   | 0     | 0.28   |
| SanDisk   | SD8TB8U-128G-1006  | 128 GB | 1       | 205   | 1     | 0.28   |
| Intel     | SSDSA2M160G2HP     | 160 GB | 1       | 513   | 4     | 0.28   |
| Transcend | TS64GMSA230S       | 64 GB  | 26      | 102   | 0     | 0.28   |
| Transcend | TS256GMSA452T      | 256 GB | 3       | 102   | 0     | 0.28   |
| SanDisk   | SD8SB8U-256G-1006  | 256 GB | 1       | 101   | 0     | 0.28   |
| Samsung   | MZNLN512HAJQ-00007 | 512 GB | 1       | 101   | 0     | 0.28   |
| Samsung   | MZNTY256HDHP-000H1 | 256 GB | 1       | 101   | 0     | 0.28   |
| Corsair   | FORCE LX SSD       | 256 GB | 1       | 100   | 0     | 0.28   |
| Drevo     | X1 pro 64G         | 64 GB  | 3       | 100   | 0     | 0.28   |
| OCZ       | PETROL             | 256 GB | 1       | 100   | 0     | 0.28   |
| Apacer    | AS350              | 128 GB | 4       | 100   | 0     | 0.28   |
| Kingston  | OM8P0S3256B-A0     | 256 GB | 3       | 99    | 0     | 0.27   |
| China     | SSD                | 128 GB | 16      | 99    | 0     | 0.27   |
| Transcend | TS32GSSD370S       | 32 GB  | 12      | 99    | 0     | 0.27   |
| ADATA     | SSD S510           | 120 GB | 1       | 1879  | 18    | 0.27   |
| EMTEC     | X250               | 512 GB | 1       | 98    | 0     | 0.27   |
| Kston     | SSD                | 64 GB  | 6       | 98    | 0     | 0.27   |
| SPCC      | SSD                | 256 GB | 18      | 101   | 1     | 0.27   |
| ADATA     | SU635              | 240 GB | 4       | 97    | 0     | 0.27   |
| Goodram   | SSDPR-CL100-120-G3 | 120 GB | 6       | 97    | 0     | 0.27   |
| KingSpec  | MT-1TB             | 1 TB   | 1       | 97    | 0     | 0.27   |
| minisf... | SSD                | 256 GB | 9       | 96    | 0     | 0.27   |
| Intenso   | SSD                | 256 GB | 2       | 96    | 0     | 0.26   |
| BlueRay   | Ultra M8V          | 256 GB | 1       | 95    | 0     | 0.26   |
| Phison    | SATA SSD           | 64 GB  | 3       | 95    | 0     | 0.26   |
| Apple     | SSD SM128E         | 121 GB | 1       | 95    | 0     | 0.26   |
| Intel     | SSDSCKGF180A4L     | 180 GB | 2       | 94    | 0     | 0.26   |
| Intel     | SSDSC2BF180A5L     | 180 GB | 1       | 188   | 1     | 0.26   |
| Samsung   | MZMTE128HMGR-000MV | 128 GB | 1       | 94    | 0     | 0.26   |
| Lite-On   | L8H-256V2G         | 256 GB | 1       | 93    | 0     | 0.26   |
| KingSpec  | MT-128             | 128 GB | 6       | 93    | 0     | 0.26   |
| Phison    | NETLIST SSD 8GB... | 8 GB   | 1       | 833   | 8     | 0.25   |
| SanDisk   | SD9SN8W-256G-1006  | 256 GB | 1       | 92    | 0     | 0.25   |
| SK hynix  | HFS480G3H2X069N    | 480 GB | 1       | 92    | 0     | 0.25   |
| Netac     | SSD                | 120 GB | 4       | 92    | 0     | 0.25   |
| Ramsta    | SSD S300 Pro       | 256 GB | 1       | 91    | 0     | 0.25   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 39      | 90    | 0     | 0.25   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 1       | 90    | 0     | 0.25   |
| Plextor   | PX-128M5M          | 128 GB | 3       | 89    | 0     | 0.25   |
| China     | PATA SSD           | 8 GB   | 1       | 89    | 0     | 0.25   |
| SanDisk   | SD8SBAT032G1122    | 32 GB  | 1       | 88    | 0     | 0.24   |
| FORESEE   | 64GB SSD           | 64 GB  | 22      | 88    | 0     | 0.24   |
| Samsung   | MZMPC128HBFU-000L1 | 128 GB | 1       | 88    | 0     | 0.24   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 1       | 88    | 0     | 0.24   |
| KingDian  | S280               | 120 GB | 2       | 88    | 0     | 0.24   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 1       | 88    | 0     | 0.24   |
| Faspeed   | K5M-32G            | 32 GB  | 4       | 87    | 0     | 0.24   |
| Timetec   | 35TTM8SSATA-128G   | 128 GB | 1       | 87    | 0     | 0.24   |
| PNY       | CS900 500GB SSD    | 500 GB | 7       | 87    | 0     | 0.24   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 1       | 87    | 0     | 0.24   |
| Protectli | 240GB mSATA        | 240 GB | 8       | 87    | 0     | 0.24   |
| ADATA     | IM2S3144-030GK     | 32 GB  | 1       | 87    | 0     | 0.24   |
| Superm... | SSD                | 64 GB  | 2       | 87    | 0     | 0.24   |
| Vaseky    | V850-64G           | 64 GB  | 2       | 86    | 0     | 0.24   |
| Samsung   | SSD PM810 2.5"     | 256 GB | 2       | 776   | 7     | 0.24   |
| KingFast  | SSD                | 32 GB  | 1       | 86    | 0     | 0.24   |
| Samsung   | MZRPC256HADR-000SO | 128 GB | 2       | 85    | 0     | 0.23   |
| Transcend | TS32GMSA370        | 32 GB  | 15      | 84    | 0     | 0.23   |
| Apacer    | APM050GMFAN-4MTM1  | 54 GB  | 1       | 84    | 0     | 0.23   |
| Lite-On   | LMT-256L9M-11 M... | 256 GB | 1       | 84    | 0     | 0.23   |
| China     | BTO-240GB          | 240 GB | 1       | 82    | 0     | 0.23   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 1       | 82    | 0     | 0.23   |
| UDinfo    | M2S                | 120 GB | 3       | 82    | 0     | 0.23   |
| China     | ESA3SMD2HTGT064GB  | 64 GB  | 1       | 82    | 0     | 0.22   |
| Intel     | SSDSA2M080G2GN     | 80 GB  | 1       | 1141  | 13    | 0.22   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 15      | 81    | 0     | 0.22   |
| Samsung   | MZMPA024HMCD-000L1 | 24 GB  | 1       | 81    | 0     | 0.22   |
| SanDisk   | SSD G5 BICS4       | 1 TB   | 6       | 80    | 0     | 0.22   |
| Kingston  | SA400M8120G        | 120 GB | 8       | 80    | 0     | 0.22   |
| Samsung   | MZNLN256HAJQ-000L7 | 256 GB | 2       | 79    | 0     | 0.22   |
| SanDisk   | SD6SF1M032G1022    | 32 GB  | 1       | 79    | 0     | 0.22   |
| Lite-On   | CV3-8D128          | 128 GB | 1       | 79    | 0     | 0.22   |
| Intenso   | JAJMS600M256G      | 256 GB | 3       | 77    | 0     | 0.21   |
| Samsung   | SSD 870 QVO        | 2 TB   | 14      | 77    | 0     | 0.21   |
| BORY      | M500 128G          | 128 GB | 3       | 77    | 0     | 0.21   |
| Intel     | SSDSC2KI128G8      | 100 GB | 2       | 77    | 0     | 0.21   |
| Samsung   | SSD 870 EVO        | 500 GB | 18      | 89    | 1     | 0.21   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 2       | 75    | 0     | 0.21   |
| Kingston  | SMSM151S3128GD     | 128 GB | 1       | 598   | 7     | 0.21   |
| Indilinx  | InM2246S3-128G     | 128 GB | 1       | 74    | 0     | 0.20   |
| Innodisk  | Corp. - mSATA 3... | 64 GB  | 1       | 74    | 0     | 0.20   |
| KingSpec  | NT-512             | 512 GB | 4       | 73    | 0     | 0.20   |
| Apple     | SSD SM0128G        | 121 GB | 3       | 73    | 0     | 0.20   |
| Goodram   | SSDPR-CX400-128-G2 | 128 GB | 1       | 73    | 0     | 0.20   |
| Mushkin   | MKNSSDTR240GB      | 240 GB | 1       | 73    | 0     | 0.20   |
| Intenso   | SATA III SSD       | 480 GB | 2       | 72    | 0     | 0.20   |
| Transcend | TS256GSSD230S      | 256 GB | 4       | 72    | 0     | 0.20   |
| Silicon   | SATA3 120GB SSD    | 120 GB | 1       | 71    | 0     | 0.20   |
| Gigaby... | GP-GSTFS31120GNTD  | 120 GB | 8       | 71    | 0     | 0.19   |
| Micron    | M600_MTFDDAV256MBF | 256 GB | 1       | 71    | 0     | 0.19   |
| Micron    | M500_MTFDDAK960MAV | 960 GB | 4       | 1695  | 270   | 0.19   |
| Lite-On   | CV8-8E128-11 SATA  | 128 GB | 3       | 70    | 0     | 0.19   |
| Intenso   | JAJM600M256C       | 256 GB | 1       | 70    | 0     | 0.19   |
| China     | 2.5 SATA SSD       | 128 GB | 1       | 70    | 0     | 0.19   |
| Kingston  | SM2280S3240G       | 240 GB | 1       | 70    | 0     | 0.19   |
| Team      | L5 LITE SSD        | 240 GB | 1       | 69    | 0     | 0.19   |
| SanDisk   | SD8SBAT-256G-1006  | 256 GB | 2       | 69    | 0     | 0.19   |
| PNY       | CS900 1TB SSD      | 1 TB   | 1       | 68    | 0     | 0.19   |
| SanDisk   | SD9TN8W256G1001    | 256 GB | 2       | 68    | 0     | 0.19   |
| Intel     | SSDSA2BW160G3H     | 160 GB | 4       | 203   | 12    | 0.19   |
| Intenso   | SSD                | 120 GB | 6       | 68    | 0     | 0.19   |
| Transcend | TS120GMTS820S      | 120 GB | 3       | 68    | 0     | 0.19   |
| Kingston  | SKC600256G         | 256 GB | 3       | 67    | 0     | 0.19   |
| Transcend | TS32GHSD370        | 32 GB  | 1       | 67    | 0     | 0.19   |
| Innodisk  | DEM24-32GM41BC1... | 32 GB  | 1       | 67    | 0     | 0.19   |
| China     | SSD                | 120 GB | 11      | 96    | 1     | 0.19   |
| Intel     | SSDSCKGF256A5 SATA | 256 GB | 1       | 67    | 0     | 0.19   |
| Drevo     | X1 SSD             | 64 GB  | 1       | 66    | 0     | 0.18   |
| Intel     | SSDSC2KG480G8      | 480 GB | 8       | 65    | 0     | 0.18   |
| OWC       | Mercury EXTREME... | 960 GB | 2       | 65    | 0     | 0.18   |
| Supers... | SUPERSONIC128GB    | 128 GB | 1       | 65    | 0     | 0.18   |
| Plextor   | PX-256M5S          | 256 GB | 2       | 64    | 0     | 0.18   |
| China     | CHESHI-128G        | 128 GB | 1       | 64    | 0     | 0.18   |
| Samsung   | SSD 870 EVO        | 250 GB | 27      | 63    | 0     | 0.17   |
| Intel     | SSDSA2BW160G3      | 160 GB | 1       | 62    | 0     | 0.17   |
| SanDisk   | SD9SN8W128G1102    | 128 GB | 2       | 62    | 0     | 0.17   |
| Transcend | TS64GSSD420K       | 64 GB  | 4       | 62    | 0     | 0.17   |
| SanDisk   | SSD P4             | 8 GB   | 1       | 62    | 0     | 0.17   |
| Apple     | SSD SM256E         | 256 GB | 5       | 222   | 25    | 0.17   |
| Samsung   | SSD 870 EVO        | 1 TB   | 20      | 152   | 8     | 0.17   |
| Transcend | TS256GMTS952T2     | 256 GB | 21      | 60    | 0     | 0.17   |
| Intel     | SSDSCKJF240A5H REF | 240 GB | 1       | 60    | 0     | 0.17   |
| Transcend | TS32GSSD370        | 32 GB  | 7       | 60    | 0     | 0.16   |
| BORY      | M500 512G          | 512 GB | 1       | 59    | 0     | 0.16   |
| Lite-On   | LSS-32L6G-HP       | 32 GB  | 1       | 59    | 0     | 0.16   |
| Samsung   | MZMTE1T0HMJH-00000 | 1 TB   | 1       | 59    | 0     | 0.16   |
| SPCC      | M.2 SSD            | 256 GB | 1       | 178   | 2     | 0.16   |
| Samsung   | MZYTE256HMHP-000L2 | 256 GB | 2       | 59    | 0     | 0.16   |
| SuperM... | SSD                | 128 GB | 2       | 59    | 0     | 0.16   |
| Lite-On   | L8H-256V2G-HP      | 256 GB | 2       | 59    | 0     | 0.16   |
| Team      | T253X2001T         | 1 TB   | 1       | 58    | 0     | 0.16   |
| Hikvision | HKVSN HS-SSD-S2... | 512 GB | 1       | 58    | 0     | 0.16   |
| Intel     | SSDSCKKF256G8 SATA | 256 GB | 2       | 57    | 0     | 0.16   |
| Transcend | TS128GSSD420K      | 128 GB | 2       | 57    | 0     | 0.16   |
| China     | SSD                | 256 GB | 7       | 68    | 2     | 0.16   |
| KIOXIA... | SATA SSD           | 480 GB | 1       | 57    | 0     | 0.16   |
| SanDisk   | SSD U100           | 32 GB  | 1       | 57    | 0     | 0.16   |
| Transcend | TS256GMSA230S      | 256 GB | 22      | 56    | 0     | 0.16   |
| Transcend | TS256GSSD320       | 256 GB | 2       | 170   | 3     | 0.16   |
| Crucial   | CT512MX100SSD1     | 512 GB | 1       | 56    | 0     | 0.16   |
| Intenso   | SSD Sata III       | 128 GB | 6       | 56    | 9     | 0.16   |
| Intenso   | JAJMS600M512G      | 512 GB | 1       | 56    | 0     | 0.15   |
| Yeyian    | VALK 3000          | 250 GB | 2       | 56    | 0     | 0.15   |
| Micron    | 5210_MTFDDAK7T6QDE | 7.6 TB | 4       | 55    | 0     | 0.15   |
| China     | NGFF 2280 256GB... | 256 GB | 6       | 55    | 0     | 0.15   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 6       | 55    | 0     | 0.15   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 1       | 55    | 0     | 0.15   |
| Transcend | TS64GMSA370        | 64 GB  | 17      | 55    | 0     | 0.15   |
| China     | SATA SSD           | 20 GB  | 2       | 55    | 0     | 0.15   |
| Lite-On   | L8H-256V2G-11 M... | 256 GB | 1       | 54    | 0     | 0.15   |
| China     | SATA3 480GB SSD    | 480 GB | 1       | 162   | 2     | 0.15   |
| Apacer    | 8GB SATA Flash ... | 8 GB   | 2       | 846   | 29    | 0.15   |
| Transcend | TS256GMTS800       | 256 GB | 1       | 53    | 0     | 0.15   |
| Kingch... | SSD                | 128 GB | 1       | 53    | 0     | 0.15   |
| LDLC      | SSD                | 64 GB  | 1       | 53    | 0     | 0.15   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 1       | 53    | 0     | 0.15   |
| ShiJi     | SSD                | 128 GB | 10      | 53    | 0     | 0.15   |
| Transcend | TS512GMTS830S      | 512 GB | 1       | 52    | 0     | 0.15   |
| Protectli | 120GB M.2          | 120 GB | 2       | 52    | 0     | 0.14   |
| Lite-On   | LGT-128M6G         | 128 GB | 1       | 52    | 0     | 0.14   |
| Zheino    | CHN mSATA01M 060   | 64 GB  | 2       | 52    | 0     | 0.14   |
| Crucial   | CT128MX100SSD1     | 128 GB | 4       | 341   | 12    | 0.14   |
| WDC       | WDS250G2B0A        | 250 GB | 2       | 51    | 0     | 0.14   |
| KingFast  | SSD                | 1 TB   | 2       | 51    | 0     | 0.14   |
| Samsung   | SSD 850            | 120 GB | 1       | 51    | 0     | 0.14   |
| Intel     | SSDSC2BW120H6      | 120 GB | 6       | 224   | 217   | 0.14   |
| Plextor   | PX-128M6S          | 128 GB | 2       | 50    | 0     | 0.14   |
| JMicron   | 605 SSD LBA48      | 16 GB  | 1       | 50    | 0     | 0.14   |
| Netac     | SSD                | 512 GB | 1       | 50    | 0     | 0.14   |
| OCZ       | VERTEX2            | 80 GB  | 1       | 50    | 0     | 0.14   |
| Lenovo    | SSD SL700 120G     | 120 GB | 1       | 50    | 0     | 0.14   |
| OCZ       | VERTEX2            | 55 GB  | 1       | 50    | 0     | 0.14   |
| BlueRay   | SSD120GM7B         | 120 GB | 1       | 984   | 19    | 0.13   |
| ADATA     | SU630              | 480 GB | 2       | 47    | 0     | 0.13   |
| KingSpec  | MT-256             | 256 GB | 1       | 47    | 0     | 0.13   |
| Samsung   | SSD 870 QVO        | 8 TB   | 1       | 47    | 0     | 0.13   |
| INNOVA... | SSD                | 1 TB   | 1       | 47    | 0     | 0.13   |
| China     | SSE256GMLCT-SBC-2S | 256 GB | 1       | 47    | 0     | 0.13   |
| Intel     | SSDSC2BF180A5H REF | 180 GB | 1       | 47    | 0     | 0.13   |
| China     | M.2 SSD            | 256 GB | 2       | 46    | 0     | 0.13   |
| Kingston  | SKC600MS256G       | 256 GB | 23      | 46    | 0     | 0.13   |
| INDMEM    | SSD mSATA          | 256 GB | 1       | 46    | 0     | 0.13   |
| Samsung   | MZ7LN128HAHQ-00000 | 128 GB | 1       | 46    | 0     | 0.13   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 2       | 46    | 0     | 0.13   |
| KingSpec  | P3-128             | 128 GB | 2       | 117   | 3     | 0.13   |
| SanDisk   | SD6PP4M-256G-1006  | 256 GB | 1       | 45    | 0     | 0.12   |
| KeepData  | GIM128             | 128 GB | 10      | 44    | 0     | 0.12   |
| China     | TYPEC 120GB PSSD   | 120 GB | 1       | 44    | 0     | 0.12   |
| KingFast  | SSD                | 256 GB | 7       | 44    | 0     | 0.12   |
| KingFast  | SSD                | 512 GB | 2       | 43    | 0     | 0.12   |
| China     | SSD 64G            | 64 GB  | 1       | 43    | 0     | 0.12   |
| ADATA     | SU800              | 512 GB | 3       | 43    | 0     | 0.12   |
| ShiJi     | SSD                | 64 GB  | 3       | 43    | 0     | 0.12   |
| Zheino    | CHN mSATAM1 064    | 64 GB  | 1       | 43    | 0     | 0.12   |
| Goodram   | SSDPR-CX400-512-G2 | 512 GB | 2       | 42    | 0     | 0.12   |
| Timetec   | 30TT253X2-256GB    | 256 GB | 1       | 42    | 0     | 0.12   |
| China     | QST8-512           | 512 GB | 1       | 42    | 0     | 0.12   |
| SanDisk   | SD8SBAT128G1122    | 128 GB | 4       | 41    | 0     | 0.11   |
| Samsung   | SSD PM871b M.2 ... | 128 GB | 2       | 41    | 0     | 0.11   |
| Kingston  | SA400S37-240GB     | 240 GB | 1       | 41    | 0     | 0.11   |
| SanDisk   | SDSSDHP256G        | 256 GB | 1       | 41    | 0     | 0.11   |
| KingDian  | S200               | 64 GB  | 4       | 44    | 253   | 0.11   |
| Dogfish   | SSD                | 120 GB | 1       | 121   | 2     | 0.11   |
| Samsung   | SSD 850 PRO        | 1 TB   | 2       | 40    | 0     | 0.11   |
| ADATA     | ASU800SS-128GT     | 128 GB | 2       | 39    | 0     | 0.11   |
| Intel     | SSDSC2KW256G8L     | 256 GB | 1       | 39    | 0     | 0.11   |
| Transcend | TS128GMSA370       | 128 GB | 21      | 39    | 0     | 0.11   |
| HPE       | MK000480GWXFF      | 480 GB | 2       | 39    | 0     | 0.11   |
| SanDisk   | SSD 128G           | 128 GB | 3       | 39    | 0     | 0.11   |
| Lite-On   | LMS-32L6M-HP       | 32 GB  | 2       | 38    | 0     | 0.10   |
| WDC       | WDS120G1G0B-00RC30 | 120 GB | 1       | 37    | 0     | 0.10   |
| Patriot   | Burst Elite        | 120 GB | 5       | 37    | 0     | 0.10   |
| Samsung   | MZ7LN256HCHP-000F0 | 256 GB | 1       | 37    | 0     | 0.10   |
| Transcend | TS256GMSA452T2     | 256 GB | 4       | 37    | 0     | 0.10   |
| WDC       | WDS200T2B0B-00YS70 | 2 TB   | 1       | 37    | 0     | 0.10   |
| Qunion    | P20A 64G           | 64 GB  | 1       | 37    | 0     | 0.10   |
| Kingston  | SUV400S37 120G     | 120 GB | 1       | 37    | 0     | 0.10   |
| Micron    | 1100 SATA          | 512 GB | 1       | 36    | 0     | 0.10   |
| SK hynix  | SC308 SATA         | 128 GB | 3       | 504   | 37    | 0.10   |
| Fujitsu   | F500S 120G         | 120 GB | 1       | 36    | 0     | 0.10   |
| KingSpec  | P3-256             | 256 GB | 1       | 35    | 0     | 0.10   |
| Phison    | SATA SSD           | 240 GB | 1       | 35    | 0     | 0.10   |
| INDMEM    | M.2 2260           | 256 GB | 1       | 35    | 0     | 0.10   |
| Intenso   | SATA3 240GB SSD    | 240 GB | 1       | 35    | 0     | 0.10   |
| China     | SSD                | 512 GB | 3       | 34    | 0     | 0.10   |
| Vaseky    | V850-128GB         | 128 GB | 2       | 34    | 0     | 0.09   |
| KingSpec  | NT-256             | 256 GB | 4       | 33    | 0     | 0.09   |
| Intenso   | SSD Sata III       | 256 GB | 4       | 33    | 0     | 0.09   |
| Protectli | 480GB M.2          | 480 GB | 1       | 33    | 0     | 0.09   |
| MidasF... | SSD                | 256 GB | 1       | 32    | 0     | 0.09   |
| OCZ       | VERTEX-TURBO       | 32 GB  | 2       | 298   | 56    | 0.09   |
| Samsung   | 470 Series SSD     | 64 GB  | 1       | 32    | 0     | 0.09   |
| OCZ       | VECTOR150          | 240 GB | 1       | 603   | 18    | 0.09   |
| SATADOM   | SH 3ME4            | 16 GB  | 1       | 31    | 0     | 0.09   |
| Transcend | TS512GMTS430S      | 512 GB | 1       | 31    | 0     | 0.09   |
| China     | KR 32G             | 32 GB  | 1       | 31    | 0     | 0.09   |
| Micron    | 5200_MTFDDAK480TDN | 480 GB | 1       | 31    | 0     | 0.09   |
| Kingston  | HyperX Fury 3D ... | 480 GB | 2       | 31    | 0     | 0.09   |
| China     | NGFF 2242 512GB... | 512 GB | 1       | 31    | 0     | 0.09   |
| Crucial   | CT480M500SSD1      | 480 GB | 4       | 1594  | 524   | 0.09   |
| China     | NGFF 2280 128GB... | 128 GB | 4       | 37    | 1     | 0.08   |
| Goodram   | SSDPR-CX400-256-G2 | 256 GB | 3       | 30    | 0     | 0.08   |
| KingDian  | S280               | 480 GB | 1       | 30    | 0     | 0.08   |
| Toshiba   | TL100              | 120 GB | 1       | 30    | 0     | 0.08   |
| Transcend | TS256GMSA370       | 256 GB | 1       | 29    | 0     | 0.08   |
| China     | R580               | 64 GB  | 1       | 29    | 0     | 0.08   |
| SanDisk   | SD8TB8U-256G-1006  | 256 GB | 2       | 763   | 514   | 0.08   |
| China     | FPT310M8SSD128G    | 128 GB | 3       | 27    | 0     | 0.08   |
| Transcend | TS128GMSA452T2     | 128 GB | 1       | 27    | 0     | 0.08   |
| Samsung   | MZNLN256HMHQ-000L7 | 256 GB | 1       | 27    | 0     | 0.08   |
| Plextor   | PX-128G7Ne         | 128 GB | 1       | 189   | 6     | 0.07   |
| Samsung   | MZ7L3240HCHQ-00A07 | 240 GB | 1       | 27    | 0     | 0.07   |
| Intel     | SSDSCKKW512G8      | 512 GB | 1       | 26    | 0     | 0.07   |
| Dogfish   | SSD                | 64 GB  | 1       | 26    | 0     | 0.07   |
| TAMMUZ    | SSD                | 32 GB  | 1       | 26    | 0     | 0.07   |
| Micron    | M550_MTFDDAK064MAY | 64 GB  | 1       | 26    | 0     | 0.07   |
| Apacer    | AS340              | 120 GB | 1       | 25    | 0     | 0.07   |
| Samsung   | SSD 870 QVO        | 1 TB   | 8       | 25    | 0     | 0.07   |
| Transcend | TS128GSSD370       | 128 GB | 1       | 25    | 0     | 0.07   |
| Lite-On   | LCH-256V2S         | 256 GB | 3       | 25    | 0     | 0.07   |
| Transcend | TS128GMTS600       | 128 GB | 1       | 24    | 0     | 0.07   |
| Verbatim  | Vi550 S3           | 128 GB | 1       | 24    | 0     | 0.07   |
| WDC       | PC SA530 SDASB8... | 256 GB | 1       | 24    | 0     | 0.07   |
| SanDisk   | SD8SNAT256G1122    | 256 GB | 1       | 23    | 0     | 0.07   |
| SHAREVDI  | 128GB SSD          | 128 GB | 12      | 23    | 0     | 0.06   |
| Lite-On   | J8-L1032-11 M.2... | 32 GB  | 1       | 23    | 0     | 0.06   |
| Lite-On   | LSS-16L6G-HP       | 16 GB  | 1       | 23    | 0     | 0.06   |
| Seagate   | IronWolf ZA1000... | 1 TB   | 1       | 23    | 0     | 0.06   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 1       | 46    | 1     | 0.06   |
| Intel     | SSDSCKKF128G8 SATA | 128 GB | 1       | 22    | 0     | 0.06   |
| China     | CS2246-M512        | 506 GB | 1       | 22    | 0     | 0.06   |
| BR        | SSD 32G            | 32 GB  | 1       | 22    | 0     | 0.06   |
| Crucial   | CT512M550SSD1      | 512 GB | 1       | 379   | 16    | 0.06   |
| ADATA     | SP550              | 240 GB | 1       | 155   | 6     | 0.06   |
| China     | SATA3 512GB SSD    | 512 GB | 1       | 22    | 0     | 0.06   |
| Transcend | TS512GMSA370       | 512 GB | 1       | 21    | 0     | 0.06   |
| China     | D128GSSDQ400S      | 128 GB | 1       | 21    | 0     | 0.06   |
| Samsung   | SSD PM810 2.5"     | 128 GB | 1       | 623   | 28    | 0.06   |
| China     | W653-64GB          | 64 GB  | 1       | 21    | 0     | 0.06   |
| SanDisk   | SSD i100           | 64 GB  | 1       | 21    | 0     | 0.06   |
| China     | SH00M128GB         | 128 GB | 2       | 22    | 4     | 0.06   |
| V-GeN     | V-GEN10AS20AR12... | 128 GB | 1       | 21    | 0     | 0.06   |
| POWER X   | SS1000-512GB       | 512 GB | 1       | 20    | 0     | 0.06   |
| Toshiba   | VT180              | 480 GB | 2       | 20    | 0     | 0.06   |
| Dogfish   | SSD                | 500 GB | 1       | 20    | 0     | 0.06   |
| Netac     | S535N8-256GYN      | 256 GB | 1       | 20    | 0     | 0.06   |
| KingFast  | SSD                | 64 GB  | 2       | 584   | 39    | 0.06   |
| ORICO     | PH100-128G         | 128 GB | 1       | 19    | 0     | 0.05   |
| Gigabyte  | GP-GSTFS31480GNTD  | 480 GB | 1       | 19    | 0     | 0.05   |
| ADATA     | ASU800SS-256GT-2   | 256 GB | 1       | 19    | 0     | 0.05   |
| ShiJi     | SSD                | 256 GB | 2       | 19    | 0     | 0.05   |
| Transcend | TS32GMTS600        | 32 GB  | 3       | 19    | 0     | 0.05   |
| SanPin    | mSATA-64GB         | 64 GB  | 1       | 19    | 0     | 0.05   |
| Lite-On   | CV3-CE128-11 SATA  | 128 GB | 1       | 19    | 0     | 0.05   |
| Zheino    | CHN HFmSATA01M 128 | 128 GB | 1       | 18    | 0     | 0.05   |
| MicroD... | 512G SSD           | 512 GB | 1       | 18    | 0     | 0.05   |
| SPCC      | SSD                | 55 GB  | 1       | 18    | 0     | 0.05   |
| ADATA     | SU655              | 240 GB | 1       | 18    | 0     | 0.05   |
| Seagate   | XA960LE10063       | 960 GB | 2       | 17    | 0     | 0.05   |
| SanDisk   | SSD P4             | 16 GB  | 2       | 86    | 4     | 0.05   |
| Micron    | 1100 SATA          | 256 GB | 9       | 32    | 126   | 0.05   |
| PNY       | 120GB SATA SSD     | 120 GB | 4       | 17    | 0     | 0.05   |
| Apacer    | 256GB SATA Flas... | 256 GB | 1       | 17    | 0     | 0.05   |
| Lite-On   | PH4-CE120          | 120 GB | 1       | 17    | 0     | 0.05   |
| BAITITON  | BT58SSD08M         | 128 GB | 3       | 16    | 0     | 0.05   |
| XPG       | SX950U             | 240 GB | 1       | 370   | 21    | 0.05   |
| Apple     | A45ACXBA9TA        | 512 GB | 1       | 16    | 0     | 0.04   |
| KingSpec  | P4-960             | 960 GB | 1       | 15    | 0     | 0.04   |
| Transcend | TS128GMTS800       | 128 GB | 2       | 15    | 0     | 0.04   |
| SanDisk   | SD8SBAT064G1122    | 64 GB  | 1       | 15    | 0     | 0.04   |
| China     | SSD                | 16 GB  | 2       | 15    | 0     | 0.04   |
| Transcend | TS256GMSA370S      | 256 GB | 3       | 15    | 0     | 0.04   |
| Lexar     | 128GB SSD          | 128 GB | 5       | 14    | 0     | 0.04   |
| PNY       | SSD2SC240G5LC70... | 240 GB | 1       | 14    | 0     | 0.04   |
| Transcend | TS256GMTS430S      | 256 GB | 7       | 14    | 0     | 0.04   |
| SETHRISE  | SSD 480G           | 480 GB | 1       | 14    | 0     | 0.04   |
| China     | SH00M240GB         | 240 GB | 1       | 14    | 0     | 0.04   |
| FORESEE   | S326M256G          | 256 GB | 1       | 14    | 0     | 0.04   |
| Leven     | JAJS600M128C       | 128 GB | 1       | 14    | 0     | 0.04   |
| Apacer    | 4GB SATA Flash ... | 4 GB   | 1       | 14    | 0     | 0.04   |
| Hikvision | HS-SSD-E100 128G   | 128 GB | 1       | 14    | 0     | 0.04   |
| SK hynix  | SC210 mSATA        | 256 GB | 3       | 305   | 54    | 0.04   |
| Apacer    | AS681              | 240 GB | 1       | 14    | 0     | 0.04   |
| HCiPC     | P2MSM-64G2B SATA3  | 64 GB  | 2       | 14    | 0     | 0.04   |
| Transcend | TS256GMTS400       | 256 GB | 1       | 14    | 0     | 0.04   |
| Lexar     | 240GB SSD          | 240 GB | 1       | 14    | 0     | 0.04   |
| Kingch... | SSD                | 64 GB  | 1       | 13    | 0     | 0.04   |
| T-FORCE   | SSD                | 1 TB   | 1       | 13    | 0     | 0.04   |
| Micron    | 5300_MTFDDAV480TDS | 480 GB | 2       | 13    | 0     | 0.04   |
| ATP       | SATA III M.2 2242  | 64 GB  | 2       | 13    | 0     | 0.04   |
| Kingston  | HyperX Fury 3D     | 120 GB | 1       | 13    | 0     | 0.04   |
| Intel     | SSDSC2BF256A5 SATA | 256 GB | 1       | 360   | 26    | 0.04   |
| ADATA     | SP610              | 128 GB | 1       | 39    | 2     | 0.04   |
| Hikvision | HS-SSD-E100N 128G  | 128 GB | 1       | 13    | 0     | 0.04   |
| Intel     | SSDSCKKR128G8      | 128 GB | 1       | 13    | 0     | 0.04   |
| Corsair   | Voyager GTX        | 256 GB | 1       | 13    | 0     | 0.04   |
| SanDisk   | SD8SBAT256G1002    | 256 GB | 2       | 12    | 0     | 0.04   |
| China     | HOM128M-46XI2      | 128 GB | 1       | 12    | 0     | 0.04   |
| Toshiba   | KSG60ZMV256G       | 256 GB | 1       | 12    | 0     | 0.03   |
| China     | SK                 | 128 GB | 2       | 12    | 0     | 0.03   |
| Hikvision | HS-SSD-C100 120G   | 120 GB | 1       | 12    | 0     | 0.03   |
| NTC       | SSD                | 120 GB | 1       | 12    | 0     | 0.03   |
| Transcend | TS512GSSD230S      | 512 GB | 1       | 12    | 0     | 0.03   |
| Intel     | SSDSC2KB480G7K     | 480 GB | 1       | 158   | 12    | 0.03   |
| Kingston  | SUV500MS-128G      | 128 GB | 1       | 12    | 0     | 0.03   |
| Netac     | SSD                | 240 GB | 1       | 12    | 0     | 0.03   |
| AirDisk   | 128GB SSD          | 128 GB | 6       | 12    | 0     | 0.03   |
| Biostar   | S100-240GB         | 240 GB | 1       | 12    | 0     | 0.03   |
| KingFast  | SSD                | 240 GB | 1       | 11    | 0     | 0.03   |
| Lite-On   | LMH-128V2M-11 M... | 128 GB | 2       | 11    | 0     | 0.03   |
| Innodisk  | 2.5" SATA SSD 3ME2 | 128 GB | 1       | 187   | 15    | 0.03   |
| Colorful  | SL500              | 640 GB | 1       | 727   | 62    | 0.03   |
| Intel     | SSDSC2KF256H6L     | 256 GB | 2       | 53    | 11    | 0.03   |
| XrayDisk  | SSD                | 256 GB | 1       | 11    | 0     | 0.03   |
| Innodisk  | CFast 3ME3         | 128 GB | 1       | 10    | 0     | 0.03   |
| Intenso   | SSD Sata III       | 240 GB | 1       | 10    | 0     | 0.03   |
| China     | SSE256GMLCT-SBC-4S | 256 GB | 1       | 10    | 0     | 0.03   |
| Hikvision | HS-SSD-C100 240G   | 240 GB | 1       | 10    | 0     | 0.03   |
| Intel     | SSDSC2KB960G8      | 960 GB | 1       | 10    | 0     | 0.03   |
| Seagate   | FireCuda 120 SS... | 2 TB   | 1       | 9     | 0     | 0.03   |
| ADATA     | SU650NS38          | 240 GB | 1       | 9     | 0     | 0.03   |
| ZTC       | MS001-128G         | 128 GB | 1       | 9     | 0     | 0.03   |
| Patriot   | Inferno 60GB SSD   | 64 GB  | 1       | 936   | 96    | 0.03   |
| Lite-On   | CS1-SP16-11 M.2... | 16 GB  | 1       | 9     | 0     | 0.03   |
| Leven     | JAJS600M512C       | 512 GB | 1       | 9     | 0     | 0.03   |
| Kingston  | SKC600MS1024G      | 1 TB   | 3       | 9     | 0     | 0.03   |
| Samsung   | MZ7LH480HBHQ0D3    | 480 GB | 2       | 9     | 0     | 0.02   |
| ADATA     | SU760              | 1 TB   | 2       | 8     | 0     | 0.02   |
| Micron    | 1300 SATA          | 512 GB | 1       | 8     | 0     | 0.02   |
| SK hynix  | HFS128G39TNF-N3A0A | 128 GB | 2       | 8     | 0     | 0.02   |
| ADATA     | SU650NS38          | 256 GB | 1       | 8     | 0     | 0.02   |
| Transcend | TS128VSDMD15LAP    | 128 GB | 1       | 8     | 0     | 0.02   |
| Indilinx  | InM2246S3-64G      | 64 GB  | 1       | 8     | 0     | 0.02   |
| EAGET     | SSD                | 120 GB | 1       | 8     | 0     | 0.02   |
| MSI       | S270               | 240 GB | 1       | 7     | 0     | 0.02   |
| Qunion    | SSD 128G           | 128 GB | 1       | 23    | 2     | 0.02   |
| Kingston  | SKC600MS512G       | 512 GB | 12      | 7     | 0     | 0.02   |
| Samsung   | SSD PM810 2.5" 7mm | 256 GB | 2       | 985   | 767   | 0.02   |
| Lite-On   | LJH-64V2G-11 M.... | 64 GB  | 1       | 38    | 4     | 0.02   |
| China     | GIM256             | 256 GB | 3       | 7     | 0     | 0.02   |
| Innodisk  | M.2 (S80) 3MG2-P   | 992 GB | 1       | 7     | 0     | 0.02   |
| EMTEC     | X150               | 120 GB | 3       | 7     | 0     | 0.02   |
| Corsair   | Force LX SSD       | 128 GB | 1       | 7     | 0     | 0.02   |
| Lite-On   | CS1-SP32-11 M.2... | 32 GB  | 2       | 12    | 2     | 0.02   |
| BHT       | WR202I0064G E70... | 64 GB  | 1       | 7     | 0     | 0.02   |
| China     | SSE128GMLCT-SBC-2S | 128 GB | 2       | 7     | 0     | 0.02   |
| China     | SSD64G             | 64 GB  | 1       | 64    | 8     | 0.02   |
| Pioneer   | APS-SL3N-240       | 240 GB | 1       | 772   | 107   | 0.02   |
| Transcend | TS240GESD240C      | 240 GB | 1       | 7     | 0     | 0.02   |
| OCZ       | VERTEX             | 32 GB  | 1       | 13    | 1     | 0.02   |
| China     | NGFF 2280 512GB... | 512 GB | 1       | 6     | 0     | 0.02   |
| China     | XJH-32GB           | 32 GB  | 1       | 26    | 3     | 0.02   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 2       | 6     | 0     | 0.02   |
| Team      | T253512GB          | 512 GB | 2       | 6     | 0     | 0.02   |
| Zheino    | CHN-mSATAQ3-120    | 120 GB | 2       | 6     | 0     | 0.02   |
| Netac     | SSD                | 256 GB | 2       | 6     | 0     | 0.02   |
| LDLC      | SSD                | 128 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 1       | 6     | 0     | 0.02   |
| Transcend | TS32GMTS800        | 32 GB  | 4       | 6     | 0     | 0.02   |
| ADATA     | ASU800SS-256GT     | 256 GB | 1       | 108   | 17    | 0.02   |
| XrayDisk  | 1TB SSD            | 1 TB   | 1       | 5     | 0     | 0.02   |
| Zheino    | CHN-mSATAM1-32     | 32 GB  | 1       | 5     | 0     | 0.02   |
| Transcend | TS16EPTMM1600L     | 16 GB  | 1       | 5     | 0     | 0.02   |
| SMI       | SSD DISK           | 120 GB | 1       | 519   | 89    | 0.02   |
| MEMXPRO   | mSATA M3B          | 32 GB  | 4       | 5     | 0     | 0.02   |
| China     | Solid              | 256 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZNLN256HMHQ-000   | 256 GB | 1       | 5     | 0     | 0.02   |
| Valuetech | SSD                | 256 GB | 2       | 5     | 0     | 0.02   |
| Leven     | JAJS300M480C       | 480 GB | 1       | 5     | 0     | 0.01   |
| Samsung   | PM881 SATA         | 256 GB | 1       | 5     | 0     | 0.01   |
| Corsair   | Force LE SSD       | 240 GB | 1       | 1471  | 285   | 0.01   |
| HP        | SSD S600           | 240 GB | 1       | 5     | 0     | 0.01   |
| Samsung   | MZMTE128HMGR-000L2 | 128 GB | 1       | 4     | 0     | 0.01   |
| KingSpec  | KSD-SA25.7-008MJ   | 8 GB   | 1       | 4     | 0     | 0.01   |
| XrayDisk  | SSD                | 128 GB | 1       | 4     | 0     | 0.01   |
| Zheino    | CHN mSATAM1 256    | 256 GB | 1       | 4     | 0     | 0.01   |
| Plextor   | PH6-CE240          | 240 GB | 1       | 4     | 0     | 0.01   |
| Transcend | TS64GMSA370S       | 64 GB  | 1       | 4     | 0     | 0.01   |
| Fordisk   | 128G 6.0Gbps ND    | 128 GB | 4       | 4     | 0     | 0.01   |
| Toshiba   | KSG60ZSE256G SATA  | 256 GB | 1       | 468   | 100   | 0.01   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 1       | 4     | 0     | 0.01   |
| MidasF... | SSD                | 120 GB | 1       | 22    | 4     | 0.01   |
| Corsair   | Neutron GTX SSD    | 120 GB | 1       | 678   | 149   | 0.01   |
| ATP       | SATA III 2.5 in... | 120 GB | 1       | 4     | 0     | 0.01   |
| Team      | T253X1240G         | 240 GB | 1       | 4     | 0     | 0.01   |
| KingDian  | M200               | 64 GB  | 1       | 4     | 0     | 0.01   |
| Toshiba   | THNSNH128GCST      | 128 GB | 1       | 4     | 0     | 0.01   |
| XrayDisk  | SSD                | 240 GB | 1       | 90    | 21    | 0.01   |
| China     | FPT310M4SSD256G    | 256 GB | 1       | 4     | 0     | 0.01   |
| INDMEM    | SSD mSATA          | 128 GB | 2       | 88    | 15    | 0.01   |
| Kingston  | OM8P0S3512F-00     | 512 GB | 1       | 4     | 0     | 0.01   |
| Verbatim  | Vi560 SATA III ... | 256 GB | 1       | 4     | 0     | 0.01   |
| Mushkin   | MKNSSDSR120GB      | 120 GB | 1       | 3     | 0     | 0.01   |
| Innodisk  | 2.5" SATA SSD 3... | 128 GB | 1       | 3     | 0     | 0.01   |
| Samsung   | SSD 870 EVO        | 4 TB   | 2       | 3     | 0     | 0.01   |
| Netac     | SSD                | 128 GB | 2       | 14    | 2     | 0.01   |
| Kingston  | SUV500M8-128GB     | 128 GB | 2       | 3     | 0     | 0.01   |
| Kingston  | OM8P0S3128B-A0     | 128 GB | 1       | 3     | 0     | 0.01   |
| Apacer    | AS220              | 256 GB | 1       | 3     | 0     | 0.01   |
| BIWIN     | SSD                | 64 GB  | 1       | 3     | 0     | 0.01   |
| KingDian  | M100               | 16 GB  | 1       | 3     | 0     | 0.01   |
| China     | GIM64              | 64 GB  | 1       | 3     | 0     | 0.01   |
| Toshiba   | THNSNK256GCS8 SATA | 256 GB | 1       | 373   | 100   | 0.01   |
| SanDisk   | SSD P4             | 64 GB  | 1       | 911   | 247   | 0.01   |
| CWDISK    | SSD                | 128 GB | 4       | 3     | 0     | 0.01   |
| FORESEE   | 256GB SSD          | 256 GB | 4       | 3     | 0     | 0.01   |
| Lite-On   | L8H-128V2G         | 128 GB | 1       | 3     | 0     | 0.01   |
| BIWIN     | SSD                | 16 GB  | 1       | 3     | 0     | 0.01   |
| ORICO     | H110-120GB-PU-EP   | 120 GB | 2       | 3     | 0     | 0.01   |
| Fanxiang  | S101               | 1 TB   | 1       | 3     | 0     | 0.01   |
| OWC       | Aura               | 960 GB | 1       | 3     | 0     | 0.01   |
| FLEXXON   | FSSO064GTTS7-M1... | 64 GB  | 1       | 3     | 0     | 0.01   |
| Lite-On   | CV1-8B512          | 512 GB | 1       | 3     | 0     | 0.01   |
| Goodram   | SSDPR-CX400-01T-G2 | 1 TB   | 1       | 3     | 0     | 0.01   |
| AMD       | R5SL120G           | 120 GB | 3       | 3     | 0     | 0.01   |
| SanDisk   | SD9SB8W128G1001    | 128 GB | 1       | 3     | 0     | 0.01   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 1       | 2998  | 1010  | 0.01   |
| SanDisk   | SD8SNAT-128G-1006  | 128 GB | 1       | 2     | 0     | 0.01   |
| Transcend | TS16GMSA370I       | 16 GB  | 1       | 2     | 0     | 0.01   |
| SanDisk   | SSD 64G            | 64 GB  | 1       | 2     | 0     | 0.01   |
| EDGE      | Boost Pro 120GB... | 120 GB | 1       | 2518  | 1020  | 0.01   |
| China     | SATA3 240GB SSD    | 240 GB | 1       | 231   | 97    | 0.01   |
| Lite-On   | LMT-32L3M          | 32 GB  | 1       | 2     | 0     | 0.01   |
| China     | XJH-64GB           | 64 GB  | 1       | 2     | 0     | 0.01   |
| China     | MSATA 32GB SSD     | 32 GB  | 5       | 2     | 0     | 0.01   |
| Transcend | TS512GMTS952T2     | 512 GB | 2       | 2     | 0     | 0.01   |
| Hikvision | HS-SSD-Minder(S... | 120 GB | 1       | 2     | 0     | 0.01   |
| Intel     | SSDSC2KB960G8L     | 960 GB | 8       | 2     | 0     | 0.01   |
| ATP       | SATA III mSATA SSD | 240 GB | 5       | 2     | 0     | 0.01   |
| Integral  | V Series SATA SSD  | 240 GB | 1       | 2     | 0     | 0.01   |
| Timetec   | MS05               | 256 GB | 1       | 2     | 0     | 0.01   |
| Goodram   | SSDPR-CL100-240-G3 | 240 GB | 1       | 2     | 0     | 0.01   |
| Toshiba   | THNSNK128GCS8 SATA | 128 GB | 2       | 206   | 100   | 0.01   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MMCRE28GFMXP-MVB   | 128 GB | 1       | 2     | 0     | 0.01   |
| Transcend | TS128GMSA370S      | 128 GB | 3       | 2     | 0     | 0.01   |
| China     | W2EM120GDTA-S71... | 120 GB | 1       | 1     | 0     | 0.01   |
| Samsung   | MZNLH512HALU-00000 | 512 GB | 1       | 1     | 0     | 0.01   |
| Intel     | SSDSC2BA200G3T     | 200 GB | 4       | 1851  | 1028  | 0.00   |
| SanDisk   | SD7UB3Q256G1001    | 256 GB | 1       | 179   | 100   | 0.00   |
| Smartbuy  | SSD                | 64 GB  | 1       | 1     | 0     | 0.00   |
| Axiom     | SSD                | 500 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | SSD UM410 Serie... | 16 GB  | 1       | 38    | 24    | 0.00   |
| ATP       | SATA III M.2 22... | 240 GB | 1       | 1     | 0     | 0.00   |
| Dogfish   | SSD                | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZ5PA064HMCD-01000 | 64 GB  | 1       | 7     | 4     | 0.00   |
| China     | sk600 128gb        | 128 GB | 1       | 1     | 0     | 0.00   |
| Kston     | SSD                | 256 GB | 2       | 1     | 0     | 0.00   |
| Wintec    | 120GB SATA3 SF2... | 120 GB | 1       | 1431  | 1017  | 0.00   |
| Intel     | SSDSC2BX200G4R     | 200 GB | 3       | 1431  | 1028  | 0.00   |
| TCSUNBOW  | M3                 | 120 GB | 1       | 1     | 0     | 0.00   |
| Seagate   | ST-MSATASSD128     | 128 GB | 1       | 1     | 0     | 0.00   |
| Zheino    | CHN-25SATAC3-120   | 120 GB | 1       | 1     | 0     | 0.00   |
| Corsair   | Neutron GTX SSD    | 240 GB | 1       | 374   | 294   | 0.00   |
| KingSpec  | P3-512-TM          | 512 GB | 1       | 1     | 0     | 0.00   |
| OCZ       | AGILITY2           | 64 GB  | 1       | 1220  | 1006  | 0.00   |
| China     | 256GB SSD          | 256 GB | 1       | 1     | 0     | 0.00   |
| Lite-On   | CV3-CE256-11 SATA  | 256 GB | 1       | 1     | 0     | 0.00   |
| BIWIN     | C6308              | 64 GB  | 1       | 1     | 0     | 0.00   |
| KingSpec  | P3-1TB             | 1 TB   | 1       | 1     | 0     | 0.00   |
| VIVA      | 400s               | 240 GB | 1       | 1     | 0     | 0.00   |
| EMTEC     | X150               | 480 GB | 1       | 1     | 0     | 0.00   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 2       | 1     | 0     | 0.00   |
| Seagate   | BarraCuda Q1 SS... | 240 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | SSD 870 EVO        | 2 TB   | 2       | 1     | 0     | 0.00   |
| Mushkin   | MKNSSDEC512GB      | 512 GB | 1       | 876   | 830   | 0.00   |
| Toshiba   | THNSNK256GVN8 M... | 256 GB | 1       | 106   | 100   | 0.00   |
| Terabit   | T50S3STMLC-256G    | 256 GB | 1       | 12    | 11    | 0.00   |
| Dogfish   | SSD                | 32 GB  | 1       | 1     | 0     | 0.00   |
| Kingston  | RBU-SNS4151S316GG2 | 16 GB  | 1       | 1     | 0     | 0.00   |
| Samsung   | SSD 860 PRO        | 4 TB   | 1       | 1     | 0     | 0.00   |
| Wibtek    | W800S 256GB SSD    | 256 GB | 1       | 1     | 0     | 0.00   |
| XUM       | HX128GSSDSATA3     | 256 GB | 1       | 1     | 0     | 0.00   |
| VisionTek | mSATA              | 120 GB | 3       | 1040  | 1019  | 0.00   |
| Corsair   | CSSD-F80GBP2       | 90 GB  | 1       | 1022  | 1008  | 0.00   |
| Kingston  | SMSM151S3-128G     | 128 GB | 1       | 1     | 0     | 0.00   |
| Netac     | W800S 256GB SSD    | 256 GB | 1       | 1     | 0     | 0.00   |
| OCZ       | TRION100           | 120 GB | 1       | 1     | 0     | 0.00   |
| Micron    | P300-MTFDBAC050SAL | 50 GB  | 1       | 1111  | 1122  | 0.00   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 2       | 87    | 93    | 0.00   |
| Kingston  | RBUSC180S3764GJ    | 64 GB  | 1       | 0     | 0     | 0.00   |
| Samsung   | MZ7LN256HAJQ-000L7 | 256 GB | 1       | 0     | 0     | 0.00   |
| ShiJi     | SSD                | 32 GB  | 1       | 38    | 40    | 0.00   |
| China     | MSATA 64GB SSD     | 64 GB  | 2       | 0     | 0     | 0.00   |
| Intel     | SSDSC1BG200G4R     | 200 GB | 2       | 922   | 1028  | 0.00   |
| Transcend | TS16GMSA370        | 16 GB  | 2       | 0     | 0     | 0.00   |
| BR        | SSD                | 512 GB | 1       | 0     | 0     | 0.00   |
| FORESEE   | 512GB SSD          | 512 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | RBUSNS8180S3512GJ  | 512 GB | 2       | 0     | 0     | 0.00   |
| Intenso   | SSDAS256           | 256 GB | 1       | 0     | 0     | 0.00   |
| SAMSWEET  | SSD SM851          | 256 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2BB012T6R     | 1.2 TB | 1       | 1667  | 2035  | 0.00   |
| Kingston  | RBU-SNS8350DES3... | 128 GB | 2       | 74    | 98    | 0.00   |
| Ramaxel   | RTFMB032RFM1EWLX   | 32 GB  | 1       | 0     | 0     | 0.00   |
| KLLISRE   | SSD                | 240 GB | 1       | 0     | 0     | 0.00   |
| XUM       | HX256GSSDSATA3     | 256 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD7SB3Q128G1001    | 128 GB | 1       | 736   | 1108  | 0.00   |
| Kingsand  | C300 32G           | 32 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS16GMSA370S       | 16 GB  | 1       | 0     | 0     | 0.00   |
| Agile     | SSD                | 128 GB | 1       | 1     | 2     | 0.00   |
| SK hynix  | SC210 2.5 7MM      | 256 GB | 1       | 534   | 1007  | 0.00   |
| Intel     | SSDSC2BB120G6R     | 120 GB | 2       | 533   | 1027  | 0.00   |
| ADATA     | ICFS332-016GW      | 16 GB  | 1       | 0     | 0     | 0.00   |
| KLEVV     | NEO N400 SSD       | 120 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 2       | 0     | 0     | 0.00   |
| ADATA     | SX300              | 128 GB | 2       | 22    | 525   | 0.00   |
| ATP       | SATA III M.2 22... | 480 GB | 2       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S316G       | 16 GB  | 4       | 446   | 1022  | 0.00   |
| ANACOMDA  | A1 120GB SSD       | 120 GB | 1       | 0     | 0     | 0.00   |
| China     | 80GB SSD           | 80 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS512GSSD370S      | 512 GB | 1       | 0     | 0     | 0.00   |
| HP Phison | PSSBN016GA27MC0    | 16 GB  | 2       | 441   | 1054  | 0.00   |
| Transcend | TS1TSSD230S        | 1 TB   | 2       | 0     | 0     | 0.00   |
| China     | MW02 128GB MSATA   | 128 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TSA                | 240 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | XM13               | 32 GB  | 1       | 347   | 1029  | 0.00   |
| Intel     | SSDSC2KB480G8      | 480 GB | 1       | 0     | 0     | 0.00   |
| China     | SK                 | 64 GB  | 1       | 0     | 0     | 0.00   |
| KingSpec  | KDM-SA.51-008GMJ   | 8 GB   | 1       | 0     | 0     | 0.00   |
| Qumo      | SSD                | 120 GB | 1       | 0     | 0     | 0.00   |
| Team      | TIM3F56064GMC104   | 64 GB  | 1       | 0     | 0     | 0.00   |
| HP Phison | PSSBN016GA27BC0    | 16 GB  | 1       | 289   | 1018  | 0.00   |
| Vaseky    | V800-64G           | 64 GB  | 1       | 0     | 0     | 0.00   |
| KingSpec  | P3-512             | 512 GB | 1       | 251   | 1014  | 0.00   |
| Kingston  | SHPM2280P2-240G    | 240 GB | 1       | 227   | 1007  | 0.00   |
| BR        | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | ZP-128GB           | 128 GB | 1       | 0     | 0     | 0.00   |
| Fanxiang  | S101               | 2 TB   | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2BX100G4      | 100 GB | 1       | 0     | 0     | 0.00   |
| Pccooler  | MSATA 64G          | 64 GB  | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 860 PRO        | 2 TB   | 1       | 0     | 0     | 0.00   |
| Team      | TIM3F56032GMC104   | 32 GB  | 1       | 0     | 0     | 0.00   |
| Toshiba   | THNSNK512GVN8      | 512 GB | 1       | 137   | 692   | 0.00   |
| Samsung   | MZMPA128HMFU-000H1 | 128 GB | 1       | 192   | 1017  | 0.00   |
| Kingston  | SNS4151S316GD      | 16 GB  | 3       | 180   | 1025  | 0.00   |
| Seagate   | IronWolf ZA500N... | 500 GB | 2       | 0     | 0     | 0.00   |
| Zheino    | CHN MSATAQ3 480    | 480 GB | 1       | 0     | 0     | 0.00   |
| Corsair   | Force LS SSD       | 240 GB | 1       | 134   | 1009  | 0.00   |
| NITRIN... | 240GB SSD RUS      | 240 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD easystore       | 480 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | THNSNX024GMNT      | 24 GB  | 1       | 0     | 2     | 0.00   |
| Transcend | TS16GMSA372M       | 16 GB  | 1       | 0     | 0     | 0.00   |
| HP Phison | PSSBN032GA27MC0    | 32 GB  | 1       | 105   | 1067  | 0.00   |
| Kingston  | SNS4151S332GD      | 32 GB  | 1       | 87    | 1022  | 0.00   |
| Intel     | SSDSC2KW120H6      | 120 GB | 1       | 2     | 29    | 0.00   |
| Brainzap  | SSD 64G            | 64 GB  | 1       | 0     | 0     | 0.00   |
| HP        | SSD S700           | 120 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SEDC500M480G       | 480 GB | 3       | 0     | 0     | 0.00   |
| Micron    | MTFDDAK128MBF-1... | 128 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD Blue SA510 2.5  | 500 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S332G       | 32 GB  | 1       | 79    | 1022  | 0.00   |
| SanDisk   | SD9SN8W-128G-1006  | 128 GB | 1       | 71    | 969   | 0.00   |
| Lite-On   | IT LST-16S9G-HP    | 16 GB  | 1       | 46    | 1022  | 0.00   |
| Micron    | MTFDDAV256TDL-1... | 256 GB | 1       | 45    | 1008  | 0.00   |
| Intel     | SSDSC2BF240A5      | 240 GB | 1       | 84    | 2017  | 0.00   |
| China     | 512GB SSD          | 512 GB | 1       | 0     | 0     | 0.00   |
| INDMEM    | M.2 2280           | 64 GB  | 1       | 0     | 0     | 0.00   |
| Intenso   | JAJMS600M1TB       | 1 TB   | 1       | 0     | 0     | 0.00   |
| Kingston  | SEDC500M1920G      | 1.9 TB | 1       | 0     | 0     | 0.00   |
| Patriot   | Burst Elite        | 480 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD8SFAT064G1122    | 64 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS32GMSA370S       | 32 GB  | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KW480H6      | 480 GB | 1       | 39    | 1010  | 0.00   |
| Lexar     | CFAST 64GB CARD    | 64 GB  | 1       | 0     | 6     | 0.00   |
| Micron    | MTFDDAT128MAM-1J2  | 128 GB | 1       | 35    | 1587  | 0.00   |
| SMI       | SSD DISK           | 506 GB | 1       | 44    | 2329  | 0.00   |
| SanDisk   | WD Green 2.5       | 240 GB | 1       | 0     | 11    | 0.00   |
| ADATA     | SP550              | 480 GB | 1       | 4     | 1326  | 0.00   |
| SSSTC     | CVB-8D128-HP       | 128 GB | 2       | 2     | 1008  | 0.00   |
| GLOWAY    | FER60GS3-S7        | 64 GB  | 1       | 2     | 1168  | 0.00   |

SSD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| G.Skill   | Unknown                | 1      | 1       | 2532  | 0     | 6.94   |
| Intel     | 710 Series SSDs        | 1      | 1       | 2121  | 0     | 5.81   |
| Toshiba   | OCZ/Toshiba Trion SSDs | 1      | 1       | 1746  | 0     | 4.79   |
| Apple     | JMicron/Maxiotek ba... | 1      | 3       | 1519  | 0     | 4.16   |
| Intel     | X25-E SSDs             | 3      | 5       | 1433  | 0     | 3.93   |
| Crucial   | Unknown                | 1      | 2       | 1406  | 0     | 3.85   |
| Crucial   | RealSSD m4/C400/P400   | 8      | 40      | 1532  | 154   | 3.81   |
| Intel     | 525 Series SSDs        | 3      | 12      | 1398  | 1     | 3.76   |
| Seagate   | Nytro XF1230 SATA SSD  | 2      | 4       | 1341  | 0     | 3.67   |
| Micro ... | Unknown                | 1      | 1       | 1297  | 0     | 3.55   |
| Superm... | Unknown                | 1      | 1       | 1295  | 0     | 3.55   |
| Intel     | 320 Series SSDs        | 10     | 38      | 1302  | 2     | 3.53   |
| ADATA     | JMicron based SSDs     | 4      | 6       | 1280  | 0     | 3.51   |
| Dell      | Certified Intel S35... | 1      | 2       | 1173  | 0     | 3.22   |
| Transcend | JMicron/Maxiotek ba... | 4      | 7       | 1150  | 0     | 3.15   |
| ADATA     | JMicron/Maxiotek ba... | 3      | 4       | 1145  | 0     | 3.14   |
| Mushkin   | SandForce Driven SSDs  | 6      | 7       | 1262  | 119   | 3.12   |
| Intel     | Dell Certified Inte... | 2      | 11      | 1096  | 0     | 3.00   |
| Intel     | 730 and DC S35x0/36... | 23     | 69      | 1349  | 149   | 2.92   |
| Patriot   | SandForce Driven SSDs  | 1      | 1       | 1039  | 0     | 2.85   |
| HPE       | Unknown                | 6      | 11      | 1061  | 1     | 2.85   |
| OCZ       | Indilinx Barefoot_2... | 8      | 16      | 1090  | 1     | 2.82   |
| Intel     | 330/335 Series SSDs    | 6      | 18      | 1508  | 2     | 2.70   |
| Toshiba   | HG5d Series            | 3      | 5       | 963   | 0     | 2.64   |
| OCZ       | SandForce Driven SSDs  | 19     | 45      | 1274  | 77    | 2.63   |
| CFD       | Unknown                | 1      | 1       | 957   | 0     | 2.62   |
| AMD       | Silicon Motion base... | 1      | 3       | 933   | 0     | 2.56   |
| OCZ       | Indilinx Barefoot b... | 3      | 5       | 1030  | 23    | 2.53   |
| Origin... | Unknown                | 1      | 1       | 900   | 0     | 2.47   |
| Intel     | S3520 Series SSDs      | 2      | 3       | 1288  | 1     | 2.46   |
| Goodram   | Phison Driven OEM SSDs | 3      | 11      | 855   | 0     | 2.34   |
| Micron    | RealSSD C300/P300      | 1      | 2       | 1551  | 503   | 2.30   |
| Unigen    | Unknown                | 1      | 1       | 833   | 0     | 2.28   |
| Toshiba   | HG3 Series             | 1      | 1       | 826   | 0     | 2.26   |
| Kingston  | JMicron/Maxiotek ba... | 4      | 7       | 1457  | 4     | 2.19   |
| Toshiba   | HG6 Series SSD         | 6      | 15      | 793   | 0     | 2.18   |
| Smart     | Unknown                | 2      | 2       | 789   | 0     | 2.16   |
| Lenovo    | Unknown                | 4      | 4       | 765   | 0     | 2.10   |
| Corsair   | SandForce Driven SSDs  | 14     | 33      | 1039  | 154   | 2.09   |
| Samsung   | Unknown                | 18     | 24      | 786   | 2     | 2.07   |
| Apple     | JMicron based SSDs     | 1      | 1       | 752   | 0     | 2.06   |
| tigo      | Unknown                | 1      | 1       | 750   | 0     | 2.06   |
| Intel     | 520 Series SSDs        | 8      | 28      | 1453  | 364   | 1.94   |
| OCZ       | Indilinx Barefoot 3... | 6      | 9       | 799   | 3     | 1.90   |
| Toshiba   | JMicron/Maxiotek ba... | 1      | 1       | 692   | 0     | 1.90   |
| Phison    | Phison Driven SSDs     | 1      | 1       | 686   | 0     | 1.88   |
| Kingston  | SandForce Driven SSDs  | 16     | 153     | 932   | 40    | 1.86   |
| Micron    | 5100 Pro / 5200 SSDs   | 1      | 5       | 736   | 1     | 1.81   |
| SuperM... | SATA DOM (SuperDOM)    | 3      | 7       | 660   | 0     | 1.81   |
| ADATA     | SandForce Driven SSDs  | 7      | 17      | 792   | 26    | 1.79   |
| Samsung   | Samsung based SSDs     | 187    | 1095    | 674   | 8     | 1.75   |
| Mach X... | Unknown                | 1      | 1       | 629   | 0     | 1.73   |
| SanDisk   | SanDisk based SSDs     | 22     | 90      | 621   | 14    | 1.63   |
| HP        | Unknown                | 11     | 18      | 577   | 0     | 1.58   |
| Crucial   | BX/MX1/2/3/500, M5/... | 5      | 13      | 668   | 1     | 1.53   |
| Silico... | Unknown                | 2      | 2       | 555   | 0     | 1.52   |
| Micron    | Client SSDs            | 15     | 31      | 593   | 1     | 1.51   |
| Advantech | Unknown                | 5      | 7       | 542   | 0     | 1.49   |
| China     | Phison Driven OEM SSDs | 10     | 140     | 561   | 3     | 1.48   |
| V-GeN     | Unknown                | 3      | 3       | 535   | 0     | 1.47   |
| Innodisk  | 1IE3/3IE3/3ME3/3IE4... | 5      | 7       | 534   | 0     | 1.46   |
| Transcend | JMicron based SSDs     | 1      | 2       | 518   | 0     | 1.42   |
| Intel     | X18-M/X25-M/X25-V G... | 7      | 21      | 1829  | 7     | 1.42   |
| Toshiba   | HG5 Series             | 1      | 2       | 508   | 0     | 1.39   |
| Toshiba   | Unknown                | 25     | 45      | 531   | 29    | 1.36   |
| Phison    | Driven OEM SSDs        | 8      | 67      | 487   | 0     | 1.34   |
| DST       | Unknown                | 1      | 1       | 485   | 0     | 1.33   |
| Intel     | 53x and Pro 1500/25... | 15     | 52      | 531   | 64    | 1.31   |
| Delkin... | Unknown                | 1      | 1       | 916   | 1     | 1.26   |
| SanDisk   | SandForce Driven SSDs  | 4      | 55      | 475   | 15    | 1.25   |
| Goodram   | Phison Driven SSDs     | 4      | 9       | 453   | 0     | 1.24   |
| Apple     | SD/SM/TS E/F/G SSDs    | 9      | 21      | 505   | 6     | 1.24   |
| Superm... | Silicon Motion base... | 2      | 3       | 450   | 0     | 1.23   |
| SATADOM   | Unknown                | 1      | 1       | 449   | 0     | 1.23   |
| AEGO      | Unknown                | 1      | 1       | 445   | 0     | 1.22   |
| BlueRay   | Unknown                | 3      | 3       | 752   | 7     | 1.21   |
| Hoodisk   | Phison Driven OEM SSDs | 5      | 177     | 435   | 0     | 1.19   |
| PNY       | Phison Driven SSDs     | 5      | 62      | 426   | 1     | 1.15   |
| KST       | Unknown                | 1      | 1       | 416   | 0     | 1.14   |
| AVEXIR    | Unknown                | 1      | 1       | 415   | 0     | 1.14   |
| Kingston  | SSDNow UV400/500       | 10     | 150     | 430   | 7     | 1.13   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 1      | 1       | 411   | 0     | 1.13   |
| Apacer    | SSDs                   | 3      | 14      | 530   | 75    | 1.12   |
| Plextor   | Unknown                | 11     | 11      | 422   | 1     | 1.12   |
| SanDisk   | Marvell based SanDi... | 45     | 154     | 434   | 2     | 1.10   |
| Patriot   | Phison Driven SSDs     | 6      | 29      | 400   | 0     | 1.10   |
| Innodisk  | Unknown                | 12     | 29      | 380   | 0     | 1.04   |
| Micron    | Unknown                | 13     | 19      | 545   | 250   | 1.02   |
| TCSUNBOW  | Unknown                | 2      | 5       | 366   | 0     | 1.00   |
| Seagate   | Unknown                | 13     | 18      | 408   | 1     | 0.98   |
| SanDisk   | Unknown                | 78     | 128     | 390   | 26    | 0.97   |
| Intel     | Unknown                | 26     | 43      | 471   | 101   | 0.97   |
| Hoodisk   | Unknown                | 1      | 3       | 332   | 0     | 0.91   |
| SK hynix  | SATA SSDs              | 14     | 38      | 459   | 40    | 0.91   |
| Smartbuy  | Phison Driven SSDs     | 4      | 6       | 331   | 0     | 0.91   |
| Mushkin   | Unknown                | 4      | 4       | 330   | 0     | 0.91   |
| Apacer    | SDM4 Series SSD Module | 2      | 29      | 441   | 16    | 0.90   |
| ADATA     | Unknown                | 22     | 64      | 325   | 34    | 0.85   |
| OWC       | SandForce Driven SSDs  | 4      | 12      | 309   | 0     | 0.85   |
| Hyundai   | Unknown                | 1      | 1       | 306   | 0     | 0.84   |
| Intel     | 545s Series SSDs       | 8      | 22      | 309   | 1     | 0.83   |
| Plextor   | M3/M5/M6/M7 Series ... | 9      | 12      | 378   | 1     | 0.82   |
| OCZ       | OCZ/Toshiba Trion SSDs | 4      | 6       | 296   | 0     | 0.81   |
| Team      | Silicon Motion base... | 2      | 3       | 294   | 0     | 0.81   |
| Patriot   | Unknown                | 7      | 11      | 378   | 9     | 0.81   |
| Faspeed   | Unknown                | 3      | 6       | 282   | 0     | 0.77   |
| Ramsta    | Silicon Motion base... | 1      | 1       | 275   | 0     | 0.75   |
| Intel     | 311/313 Series SSDs    | 1      | 1       | 269   | 0     | 0.74   |
| Apple     | Unknown                | 2      | 2       | 268   | 0     | 0.74   |
| SK hynix  | Unknown                | 8      | 13      | 320   | 26    | 0.73   |
| MyDigi... | Unknown                | 2      | 4       | 490   | 2     | 0.73   |
| Micron    | RealSSD m4/C400/P400   | 5      | 12      | 271   | 85    | 0.73   |
| Crucial   | Client SSDs            | 33     | 391     | 323   | 22    | 0.73   |
| Corsair   | Indilinx Barefoot b... | 2      | 2       | 263   | 0     | 0.72   |
| SPCC      | Phison Driven OEM SSDs | 7      | 88      | 258   | 1     | 0.70   |
| ASENNO    | Unknown                | 1      | 1       | 254   | 0     | 0.70   |
| Gigaby... | Unknown                | 1      | 2       | 252   | 0     | 0.69   |
| KingFast  | Unknown                | 6      | 30      | 285   | 33    | 0.68   |
| Seagate   | IronWolf 110 SATA SSD  | 1      | 1       | 243   | 0     | 0.67   |
| MAXIMUS   | Unknown                | 1      | 1       | 242   | 0     | 0.66   |
| Intel     | S4510/S4610/S4500/S... | 10     | 51      | 265   | 1     | 0.66   |
| Crucial   | BX/MX1/2/3/500, M5/... | 1      | 5       | 739   | 4     | 0.66   |
| Kingston  | Phison Driven SSDs     | 16     | 295     | 244   | 1     | 0.65   |
| WDC       | Blue / Red / Green ... | 27     | 222     | 253   | 5     | 0.65   |
| Team      | Unknown                | 13     | 16      | 236   | 0     | 0.65   |
| Micron    | BX/MX1/2/3/500, M5/... | 4      | 16      | 233   | 71    | 0.62   |
| Smartbuy  | Unknown                | 1      | 1       | 224   | 0     | 0.61   |
| Integral  | Unknown                | 2      | 4       | 221   | 0     | 0.61   |
| KingFast  | Silicon Motion base... | 3      | 14      | 219   | 0     | 0.60   |
| TEXTORM   | Unknown                | 1      | 1       | 214   | 0     | 0.59   |
| Indilinx  | Unknown                | 3      | 3       | 211   | 0     | 0.58   |
| Pioneer   | Unknown                | 3      | 4       | 401   | 27    | 0.58   |
| Wicgtyp   | Unknown                | 1      | 2       | 207   | 0     | 0.57   |
| KIOXIA... | Unknown                | 2      | 2       | 201   | 0     | 0.55   |
| JWX       | Unknown                | 1      | 1       | 200   | 0     | 0.55   |
| Apacer    | Unknown                | 12     | 18      | 246   | 1     | 0.54   |
| Kingston  | Unknown                | 42     | 94      | 225   | 79    | 0.54   |
| Toshiba   | OCZ                    | 3      | 4       | 194   | 0     | 0.53   |
| Vaseky    | Unknown                | 7      | 9       | 193   | 0     | 0.53   |
| Micron    | 5100 Pro / 52x0 / 5... | 4      | 6       | 192   | 0     | 0.53   |
| KimMiDi   | Unknown                | 1      | 1       | 186   | 0     | 0.51   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 1      | 7       | 185   | 0     | 0.51   |
| Silico... | Unknown                | 1      | 1       | 184   | 0     | 0.50   |
| Intenso   | Unknown                | 15     | 42      | 184   | 2     | 0.50   |
| Protectli | Unknown                | 9      | 52      | 179   | 0     | 0.49   |
| Apacer    | AS340 SSDs             | 2      | 6       | 179   | 0     | 0.49   |
| Intel     | Dell Certified Inte... | 2      | 3       | 178   | 0     | 0.49   |
| ADATA     | Silicon Motion base... | 14     | 83      | 214   | 61    | 0.49   |
| Gigastone | Unknown                | 1      | 1       | 178   | 0     | 0.49   |
| Kston     | Unknown                | 4      | 22      | 188   | 1     | 0.49   |
| Mushkin   | Silicon Motion base... | 3      | 4       | 174   | 0     | 0.48   |
| KingSpec  | Unknown                | 17     | 28      | 188   | 37    | 0.48   |
| Intenso   | Phison Driven OEM SSDs | 2      | 18      | 172   | 0     | 0.47   |
| Goodram   | Unknown                | 10     | 19      | 165   | 0     | 0.45   |
| VICK      | Unknown                | 1      | 2       | 161   | 0     | 0.44   |
| Lite-On   | Unknown                | 37     | 51      | 163   | 60    | 0.44   |
| ORICO     | Unknown                | 4      | 5       | 156   | 0     | 0.43   |
| Dogfish   | Unknown                | 9      | 15      | 190   | 1     | 0.42   |
| Corsair   | Unknown                | 6      | 6       | 569   | 122   | 0.41   |
| KingSpec  | JMicron/Maxiotek ba... | 5      | 13      | 146   | 0     | 0.40   |
| BIWIN     | Unknown                | 6      | 33      | 174   | 8     | 0.40   |
| SPCC      | Unknown                | 4      | 8       | 160   | 1     | 0.40   |
| Intel     | 510 Series SSDs        | 1      | 3       | 144   | 0     | 0.40   |
| KUIJIA    | Unknown                | 1      | 1       | 143   | 0     | 0.39   |
| Phison    | Unknown                | 2      | 2       | 513   | 4     | 0.39   |
| Dogfish   | Silicon Motion base... | 3      | 32      | 152   | 1     | 0.39   |
| Gigabyte  | Unknown                | 1      | 1       | 141   | 0     | 0.39   |
| Transcend | Unknown                | 25     | 68      | 148   | 16    | 0.38   |
| Transcend | Silicon Motion base... | 45     | 287     | 135   | 0     | 0.37   |
| minisf... | Unknown                | 2      | 13      | 129   | 0     | 0.35   |
| Marvell   | based SanDisk SSDs     | 1      | 1       | 1410  | 10    | 0.35   |
| Apple     | MacBook Air SSD        | 1      | 1       | 128   | 0     | 0.35   |
| WDC       | Blue and Green SSDs    | 3      | 10      | 126   | 0     | 0.35   |
| WDC       | Unknown                | 3      | 3       | 125   | 0     | 0.35   |
| KingDian  | Silicon Motion base... | 5      | 10      | 125   | 101   | 0.34   |
| Inland    | Unknown                | 1      | 1       | 121   | 0     | 0.33   |
| Ramaxel   | Unknown                | 2      | 2       | 118   | 0     | 0.32   |
| Intenso   | Silicon Motion base... | 2      | 4       | 117   | 0     | 0.32   |
| Pccooler  | Unknown                | 2      | 3       | 117   | 0     | 0.32   |
| Verbatim  | Unknown                | 4      | 10      | 117   | 0     | 0.32   |
| XUNZHE    | Unknown                | 1      | 1       | 106   | 0     | 0.29   |
| FORESEE   | Unknown                | 6      | 76      | 105   | 0     | 0.29   |
| Star D... | Unknown                | 1      | 1       | 105   | 0     | 0.29   |
| China     | Unknown                | 84     | 160     | 108   | 1     | 0.28   |
| Gigaby... | Phison Driven SSDs     | 2      | 10      | 102   | 0     | 0.28   |
| Corsair   | Silicon Motion base... | 1      | 1       | 100   | 0     | 0.28   |
| UDinfo    | Unknown                | 2      | 4       | 99    | 0     | 0.27   |
| CWDISK    | Unknown                | 2      | 5       | 93    | 0     | 0.26   |
| PNY       | Unknown                | 9      | 24      | 92    | 0     | 0.25   |
| Drevo     | Silicon Motion base... | 2      | 4       | 92    | 0     | 0.25   |
| BR        | Unknown                | 5      | 5       | 91    | 0     | 0.25   |
| Ramsta    | Unknown                | 1      | 1       | 91    | 0     | 0.25   |
| ZTC       | Unknown                | 2      | 3       | 430   | 9     | 0.23   |
| Lexar     | Unknown                | 3      | 3       | 85    | 2     | 0.23   |
| KingDian  | Unknown                | 3      | 3       | 83    | 0     | 0.23   |
| Zheino    | Unknown                | 9      | 12      | 76    | 0     | 0.21   |
| BORY      | Unknown                | 2      | 4       | 72    | 0     | 0.20   |
| Silicon   | Motion based OEM SSDs  | 1      | 1       | 71    | 0     | 0.20   |
| Micron    | BX/MX1/2/3/500, M5/... | 1      | 4       | 1695  | 270   | 0.19   |
| Kingch... | Unknown                | 3      | 3       | 165   | 1     | 0.19   |
| Leven     | Unknown                | 5      | 7       | 69    | 0     | 0.19   |
| Kingston  | Silicon Motion base... | 1      | 3       | 67    | 0     | 0.19   |
| Netac     | Unknown                | 8      | 13      | 68    | 1     | 0.18   |
| Supers... | Unknown                | 1      | 1       | 65    | 0     | 0.18   |
| Plextor   | M3/M5/M6 Series SSDs   | 1      | 2       | 64    | 0     | 0.18   |
| Fordisk   | Unknown                | 2      | 5       | 60    | 0     | 0.17   |
| LDLC      | Unknown                | 3      | 3       | 57    | 0     | 0.16   |
| Transcend | SandForce Driven SSDs  | 1      | 2       | 170   | 3     | 0.16   |
| Yeyian    | Unknown                | 1      | 2       | 56    | 0     | 0.15   |
| AMD       | Unknown                | 2      | 6       | 76    | 4     | 0.15   |
| XrayDisk  | Unknown                | 5      | 5       | 72    | 5     | 0.15   |
| JMicron   | Unknown                | 1      | 1       | 50    | 0     | 0.14   |
| ATP       | Unknown                | 6      | 16      | 49    | 0     | 0.14   |
| BAITITON  | Unknown                | 2      | 4       | 49    | 0     | 0.13   |
| EMTEC     | Unknown                | 4      | 6       | 47    | 0     | 0.13   |
| INNOVA... | Unknown                | 1      | 1       | 47    | 0     | 0.13   |
| KeepData  | Unknown                | 1      | 10      | 44    | 0     | 0.12   |
| Timetec   | Unknown                | 3      | 3       | 44    | 0     | 0.12   |
| ShiJi     | Unknown                | 4      | 16      | 46    | 3     | 0.12   |
| Apacer    | SDM5/5A/5A-M Series... | 2      | 3       | 569   | 20    | 0.11   |
| Gigabyte  | Phison Driven SSDs     | 3      | 3       | 36    | 0     | 0.10   |
| Fujitsu   | Unknown                | 1      | 1       | 36    | 0     | 0.10   |
| SATADOM   | Innodisk 1IE3/3IE3/... | 1      | 1       | 31    | 0     | 0.09   |
| TAMMUZ    | Unknown                | 1      | 1       | 26    | 0     | 0.07   |
| SHAREVDI  | Unknown                | 1      | 12      | 23    | 0     | 0.06   |
| Qunion    | Unknown                | 2      | 2       | 30    | 1     | 0.06   |
| POWER X   | Unknown                | 1      | 1       | 20    | 0     | 0.06   |
| SanPin    | Unknown                | 1      | 1       | 19    | 0     | 0.05   |
| MidasF... | Unknown                | 2      | 2       | 27    | 2     | 0.05   |
| Hikvision | Unknown                | 6      | 6       | 18    | 0     | 0.05   |
| MicroD... | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| INDMEM    | Unknown                | 4      | 5       | 51    | 6     | 0.05   |
| Seagate   | Nytro SATA SSD         | 1      | 2       | 17    | 0     | 0.05   |
| XPG       | Unknown                | 1      | 1       | 370   | 21    | 0.05   |
| Lexar     | 128GB SSD              | 1      | 5       | 14    | 0     | 0.04   |
| SETHRISE  | Unknown                | 1      | 1       | 14    | 0     | 0.04   |
| HCiPC     | Unknown                | 1      | 2       | 14    | 0     | 0.04   |
| T-FORCE   | Unknown                | 1      | 1       | 13    | 0     | 0.04   |
| NTC       | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| AirDisk   | Unknown                | 1      | 6       | 12    | 0     | 0.03   |
| Biostar   | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| Lite-On   | Silicon Motion base... | 1      | 2       | 11    | 0     | 0.03   |
| Colorful  | Unknown                | 1      | 1       | 727   | 62    | 0.03   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 2      | 2       | 97    | 8     | 0.03   |
| EAGET     | Unknown                | 1      | 1       | 8     | 0     | 0.02   |
| MSI       | Unknown                | 1      | 1       | 7     | 0     | 0.02   |
| BHT       | Unknown                | 1      | 1       | 7     | 0     | 0.02   |
| MEMXPRO   | Unknown                | 1      | 4       | 5     | 0     | 0.02   |
| Valuetech | Unknown                | 1      | 2       | 5     | 0     | 0.02   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 1      | 1       | 3     | 0     | 0.01   |
| OWC       | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| FLEXXON   | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| SMI       | Unknown                | 2      | 2       | 282   | 1209  | 0.01   |
| EDGE      | Unknown                | 1      | 1       | 2518  | 1020  | 0.01   |
| Fanxiang  | Unknown                | 2      | 2       | 1     | 0     | 0.00   |
| Axiom     | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Wintec    | Unknown                | 1      | 1       | 1431  | 1017  | 0.00   |
| TCSUNBOW  | Silicon Motion base... | 1      | 1       | 1     | 0     | 0.00   |
| VIVA      | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Terabit   | Unknown                | 1      | 1       | 12    | 11    | 0.00   |
| Wibtek    | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| VisionTek | Unknown                | 1      | 3       | 1040  | 1019  | 0.00   |
| XUM       | Unknown                | 2      | 2       | 0     | 0     | 0.00   |
| SAMSWEET  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| KLLISRE   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Kingsand  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Agile     | Unknown                | 1      | 1       | 1     | 2     | 0.00   |
| KLEVV     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| ANACOMDA  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison | Unknown                | 3      | 4       | 319   | 1048  | 0.00   |
| Qumo      | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| NITRIN... | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Brainzap  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Intel     | 540 Series SSDs        | 2      | 2       | 20    | 520   | 0.00   |
| SSSTC     | Unknown                | 1      | 2       | 2     | 1008  | 0.00   |
| GLOWAY    | Unknown                | 1      | 1       | 2     | 1168  | 0.00   |

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
| G.Skill     | 1      | 1       | 2532  | 0     | 6.94   |
| Micro Ce... | 1      | 1       | 1297  | 0     | 3.55   |
| Dell        | 1      | 2       | 1173  | 0     | 3.22   |
| HPE         | 6      | 11      | 1061  | 1     | 2.85   |
| CFD         | 1      | 1       | 957   | 0     | 2.62   |
| Origin I... | 1      | 1       | 900   | 0     | 2.47   |
| OCZ         | 40     | 81      | 1097  | 45    | 2.45   |
| Unigen      | 1      | 1       | 833   | 0     | 2.28   |
| Smart       | 2      | 2       | 789   | 0     | 2.16   |
| Lenovo      | 4      | 4       | 765   | 0     | 2.10   |
| tigo        | 1      | 1       | 750   | 0     | 2.06   |
| Intel       | 130    | 383     | 941   | 77    | 1.94   |
| Mushkin     | 13     | 15      | 723   | 56    | 1.82   |
| Supermicro  | 3      | 4       | 661   | 0     | 1.81   |
| SuperMicro  | 3      | 7       | 660   | 0     | 1.81   |
| Samsung     | 205    | 1119    | 677   | 8     | 1.76   |
| Corsair     | 23     | 42      | 912   | 138   | 1.74   |
| Mach Xtreme | 1      | 1       | 629   | 0     | 1.73   |
| Toshiba     | 41     | 74      | 617   | 18    | 1.63   |
| HP          | 11     | 18      | 577   | 0     | 1.58   |
| Silicon ... | 2      | 2       | 555   | 0     | 1.52   |
| Apple       | 14     | 28      | 592   | 5     | 1.51   |
| Advantech   | 5      | 7       | 542   | 0     | 1.49   |
| V-GeN       | 3      | 3       | 535   | 0     | 1.47   |
| DST         | 1      | 1       | 485   | 0     | 1.33   |
| Seagate     | 17     | 25      | 519   | 1     | 1.33   |
| Phison      | 11     | 70      | 491   | 1     | 1.32   |
| Delkin D... | 1      | 1       | 916   | 1     | 1.26   |
| AEGO        | 1      | 1       | 445   | 0     | 1.22   |
| BlueRay     | 3      | 3       | 752   | 7     | 1.21   |
| SanDisk     | 149    | 427     | 466   | 13    | 1.19   |
| Hoodisk     | 6      | 180     | 433   | 0     | 1.19   |
| Goodram     | 17     | 39      | 426   | 0     | 1.17   |
| KST         | 1      | 1       | 416   | 0     | 1.14   |
| AVEXIR      | 1      | 1       | 415   | 0     | 1.14   |
| Micron      | 44     | 95      | 531   | 95    | 1.08   |
| Patriot     | 14     | 41      | 409   | 3     | 1.06   |
| Innodisk    | 21     | 40      | 384   | 1     | 1.04   |
| Crucial     | 48     | 451     | 450   | 33    | 1.04   |
| Kingston    | 89     | 702     | 442   | 21    | 1.02   |
| AMD         | 3      | 9       | 362   | 3     | 0.95   |
| ADATA       | 50     | 174     | 369   | 44    | 0.92   |
| PNY         | 14     | 86      | 333   | 1     | 0.90   |
| Plextor     | 21     | 25      | 373   | 1     | 0.90   |
| Smartbuy    | 5      | 7       | 316   | 0     | 0.87   |
| SK hynix    | 22     | 51      | 424   | 37    | 0.86   |
| China       | 94     | 300     | 319   | 2     | 0.84   |
| Hyundai     | 1      | 1       | 306   | 0     | 0.84   |
| TCSUNBOW    | 3      | 6       | 305   | 0     | 0.84   |
| OWC         | 5      | 13      | 286   | 0     | 0.78   |
| Apacer      | 21     | 70      | 392   | 23    | 0.78   |
| Faspeed     | 3      | 6       | 282   | 0     | 0.77   |
| MyDigita... | 2      | 4       | 490   | 2     | 0.73   |
| ASENNO      | 1      | 1       | 254   | 0     | 0.70   |
| SPCC        | 11     | 96      | 250   | 1     | 0.68   |
| Team        | 15     | 19      | 245   | 0     | 0.67   |
| MAXIMUS     | 1      | 1       | 242   | 0     | 0.66   |
| KingFast    | 9      | 44      | 264   | 23    | 0.65   |
| WDC         | 33     | 235     | 246   | 5     | 0.63   |
| Integral    | 2      | 4       | 221   | 0     | 0.61   |
| TEXTORM     | 1      | 1       | 214   | 0     | 0.59   |
| Indilinx    | 3      | 3       | 211   | 0     | 0.58   |
| Pioneer     | 3      | 4       | 401   | 27    | 0.58   |
| Wicgtyp     | 1      | 2       | 207   | 0     | 0.57   |
| KIOXIA-E... | 2      | 2       | 201   | 0     | 0.55   |
| JWX         | 1      | 1       | 200   | 0     | 0.55   |
| SATADOM     | 3      | 9       | 197   | 0     | 0.54   |
| Vaseky      | 7      | 9       | 193   | 0     | 0.53   |
| KimMiDi     | 1      | 1       | 186   | 0     | 0.51   |
| Silicon ... | 1      | 1       | 184   | 0     | 0.50   |
| Ramsta      | 2      | 2       | 183   | 0     | 0.50   |
| Protectli   | 9      | 52      | 179   | 0     | 0.49   |
| Gigastone   | 1      | 1       | 178   | 0     | 0.49   |
| Kston       | 4      | 22      | 188   | 1     | 0.49   |
| Intenso     | 19     | 64      | 176   | 1     | 0.48   |
| KingSpec    | 22     | 41      | 174   | 25    | 0.45   |
| VICK        | 1      | 2       | 161   | 0     | 0.44   |
| Transcend   | 76     | 366     | 159   | 3     | 0.43   |
| ORICO       | 4      | 5       | 156   | 0     | 0.43   |
| Lite-On     | 38     | 53      | 157   | 58    | 0.43   |
| BIWIN       | 6      | 33      | 174   | 8     | 0.40   |
| Dogfish     | 12     | 47      | 164   | 1     | 0.40   |
| KUIJIA      | 1      | 1       | 143   | 0     | 0.39   |
| minisforum  | 2      | 13      | 129   | 0     | 0.35   |
| Marvell     | 1      | 1       | 1410  | 10    | 0.35   |
| Gigabyte... | 3      | 12      | 127   | 0     | 0.35   |
| Inland      | 1      | 1       | 121   | 0     | 0.33   |
| Ramaxel     | 2      | 2       | 118   | 0     | 0.32   |
| Pccooler    | 2      | 3       | 117   | 0     | 0.32   |
| Verbatim    | 4      | 10      | 117   | 0     | 0.32   |
| KingDian    | 8      | 13      | 115   | 78    | 0.31   |
| XUNZHE      | 1      | 1       | 106   | 0     | 0.29   |
| FORESEE     | 6      | 76      | 105   | 0     | 0.29   |
| Star Drive  | 1      | 1       | 105   | 0     | 0.29   |
| UDinfo      | 2      | 4       | 99    | 0     | 0.27   |
| CWDISK      | 2      | 5       | 93    | 0     | 0.26   |
| Drevo       | 2      | 4       | 92    | 0     | 0.25   |
| BR          | 5      | 5       | 91    | 0     | 0.25   |
| ZTC         | 2      | 3       | 430   | 9     | 0.23   |
| Zheino      | 9      | 12      | 76    | 0     | 0.21   |
| BORY        | 2      | 4       | 72    | 0     | 0.20   |
| Silicon     | 1      | 1       | 71    | 0     | 0.20   |
| Kingchuxing | 3      | 3       | 165   | 1     | 0.19   |
| Leven       | 5      | 7       | 69    | 0     | 0.19   |
| Netac       | 8      | 13      | 68    | 1     | 0.18   |
| Supersonic  | 1      | 1       | 65    | 0     | 0.18   |
| Gigabyte    | 4      | 4       | 62    | 0     | 0.17   |
| Fordisk     | 2      | 5       | 60    | 0     | 0.17   |
| LDLC        | 3      | 3       | 57    | 0     | 0.16   |
| Yeyian      | 1      | 2       | 56    | 0     | 0.15   |
| XrayDisk    | 5      | 5       | 72    | 5     | 0.15   |
| JMicron     | 1      | 1       | 50    | 0     | 0.14   |
| ATP         | 6      | 16      | 49    | 0     | 0.14   |
| BAITITON    | 2      | 4       | 49    | 0     | 0.13   |
| EMTEC       | 4      | 6       | 47    | 0     | 0.13   |
| INNOVATI... | 1      | 1       | 47    | 0     | 0.13   |
| KeepData    | 1      | 10      | 44    | 0     | 0.12   |
| Timetec     | 3      | 3       | 44    | 0     | 0.12   |
| ShiJi       | 4      | 16      | 46    | 3     | 0.12   |
| Lexar       | 4      | 8       | 41    | 1     | 0.11   |
| Fujitsu     | 1      | 1       | 36    | 0     | 0.10   |
| TAMMUZ      | 1      | 1       | 26    | 0     | 0.07   |
| SHAREVDI    | 1      | 12      | 23    | 0     | 0.06   |
| Qunion      | 2      | 2       | 30    | 1     | 0.06   |
| POWER X     | 1      | 1       | 20    | 0     | 0.06   |
| SanPin      | 1      | 1       | 19    | 0     | 0.05   |
| MidasForce  | 2      | 2       | 27    | 2     | 0.05   |
| Hikvision   | 6      | 6       | 18    | 0     | 0.05   |
| MicroDream  | 1      | 1       | 18    | 0     | 0.05   |
| INDMEM      | 4      | 5       | 51    | 6     | 0.05   |
| XPG         | 1      | 1       | 370   | 21    | 0.05   |
| SETHRISE    | 1      | 1       | 14    | 0     | 0.04   |
| HCiPC       | 1      | 2       | 14    | 0     | 0.04   |
| T-FORCE     | 1      | 1       | 13    | 0     | 0.04   |
| NTC         | 1      | 1       | 12    | 0     | 0.03   |
| AirDisk     | 1      | 6       | 12    | 0     | 0.03   |
| Biostar     | 1      | 1       | 12    | 0     | 0.03   |
| Colorful    | 1      | 1       | 727   | 62    | 0.03   |
| EAGET       | 1      | 1       | 8     | 0     | 0.02   |
| MSI         | 1      | 1       | 7     | 0     | 0.02   |
| BHT         | 1      | 1       | 7     | 0     | 0.02   |
| MEMXPRO     | 1      | 4       | 5     | 0     | 0.02   |
| Valuetech   | 1      | 2       | 5     | 0     | 0.02   |
| FLEXXON     | 1      | 1       | 3     | 0     | 0.01   |
| SMI         | 2      | 2       | 282   | 1209  | 0.01   |
| EDGE        | 1      | 1       | 2518  | 1020  | 0.01   |
| Fanxiang    | 2      | 2       | 1     | 0     | 0.00   |
| Axiom       | 1      | 1       | 1     | 0     | 0.00   |
| Wintec      | 1      | 1       | 1431  | 1017  | 0.00   |
| VIVA        | 1      | 1       | 1     | 0     | 0.00   |
| Terabit     | 1      | 1       | 12    | 11    | 0.00   |
| Wibtek      | 1      | 1       | 1     | 0     | 0.00   |
| VisionTek   | 1      | 3       | 1040  | 1019  | 0.00   |
| XUM         | 2      | 2       | 0     | 0     | 0.00   |
| SAMSWEET    | 1      | 1       | 0     | 0     | 0.00   |
| KLLISRE     | 1      | 1       | 0     | 0     | 0.00   |
| Kingsand    | 1      | 1       | 0     | 0     | 0.00   |
| Agile       | 1      | 1       | 1     | 2     | 0.00   |
| KLEVV       | 1      | 1       | 0     | 0     | 0.00   |
| ANACOMDA    | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison   | 3      | 4       | 319   | 1048  | 0.00   |
| Qumo        | 1      | 1       | 0     | 0     | 0.00   |
| NITRINOnet  | 1      | 1       | 0     | 0     | 0.00   |
| Brainzap    | 1      | 1       | 0     | 0     | 0.00   |
| SSSTC       | 1      | 2       | 2     | 1008  | 0.00   |
| GLOWAY      | 1      | 1       | 2     | 1168  | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| ADATA     | SX8000NP           | 256 GB | 1       | 1419  | 0     | 3.89   |
| Intel     | SSDPEDMW400G4      | 400 GB | 2       | 1410  | 0     | 3.86   |
| Samsung   | SSD 950 PRO        | 512 GB | 3       | 1357  | 0     | 3.72   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 1       | 1333  | 0     | 3.65   |
| Plextor   | PX-256M8PeY        | 256 GB | 1       | 1218  | 0     | 3.34   |
| Intel     | SSDPEDME016T4S     | 1.6 TB | 1       | 1203  | 0     | 3.30   |
| Intel     | SSDPE2MX450G7      | 450 GB | 2       | 1077  | 0     | 2.95   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 3       | 1053  | 0     | 2.89   |
| Intel     | SSDPED1D280GA      | 280 GB | 2       | 1027  | 0     | 2.81   |
| Samsung   | MZVPV256HDGL-000L7 | 256 GB | 1       | 969   | 0     | 2.66   |
| Kingston  | SKC1000240G        | 240 GB | 1       | 934   | 0     | 2.56   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 3       | 895   | 0     | 2.45   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 1       | 827   | 0     | 2.27   |
| Plextor   | PX-256M8PeG        | 256 GB | 1       | 825   | 0     | 2.26   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 2       | 804   | 0     | 2.20   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 2       | 794   | 0     | 2.18   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 2       | 765   | 0     | 2.10   |
| Samsung   | SSD 950 PRO        | 256 GB | 1       | 1495  | 1     | 2.05   |
| Transcend | TS256GMTE110S      | 256 GB | 1       | 730   | 0     | 2.00   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 1       | 718   | 0     | 1.97   |
| HP        | SSD EX900          | 120 GB | 2       | 707   | 0     | 1.94   |
| SK hynix  | PC601 NVMe         | 512 GB | 1       | 693   | 0     | 1.90   |
| Intel     | SSDPED1D480GA      | 480 GB | 1       | 597   | 0     | 1.64   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 3       | 561   | 0     | 1.54   |
| Samsung   | MZFLV512HCJH-000MV | 512 GB | 1       | 554   | 0     | 1.52   |
| Intel     | SSDPE21D280GA      | 280 GB | 2       | 543   | 0     | 1.49   |
| Phison    | Sabrent Rocket 4.0 | 500 GB | 1       | 510   | 0     | 1.40   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 6       | 504   | 0     | 1.38   |
| Intel     | SSDPEKNW010T8H     | 1 TB   | 1       | 494   | 0     | 1.36   |
| Intel     | SSDPEKKW128G8      | 128 GB | 2       | 494   | 0     | 1.35   |
| Patriot   | Scorch M2          | 128 GB | 1       | 493   | 0     | 1.35   |
| EAGET     | S900L SSD          | 128 GB | 1       | 493   | 0     | 1.35   |
| Intel     | SSDPEKKW256G8      | 256 GB | 3       | 490   | 0     | 1.34   |
| Silico... | Asgard AN2+ 256... | 256 GB | 1       | 482   | 0     | 1.32   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 2       | 449   | 0     | 1.23   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 3       | 447   | 0     | 1.23   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 1       | 446   | 0     | 1.22   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 3       | 439   | 0     | 1.20   |
| KIOXIA    | KBG30ZMV256G       | 256 GB | 1       | 435   | 0     | 1.19   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 2       | 429   | 0     | 1.18   |
| Phison    | ASE8NVME512        | 512 GB | 1       | 427   | 0     | 1.17   |
| Samsung   | PM991 NVMe         | 128 GB | 1       | 426   | 0     | 1.17   |
| Intel     | SSDPEKKW128G7      | 128 GB | 2       | 840   | 1     | 1.15   |
| SK hynix  | BC501 NVMe         | 512 GB | 1       | 409   | 0     | 1.12   |
| Reletech  | P400 M.2 Pro Q2... | 2 TB   | 1       | 403   | 0     | 1.11   |
| Kingston  | SEDC1000BM8240G    | 240 GB | 3       | 390   | 0     | 1.07   |
| HP        | SSD EX920          | 512 GB | 2       | 379   | 0     | 1.04   |
| Samsung   | SSD 960 EVO        | 250 GB | 21      | 379   | 0     | 1.04   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 2       | 378   | 0     | 1.04   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 3       | 378   | 0     | 1.04   |
| SPCC      | M.2 PCIE SSD       | 256 GB | 1       | 376   | 0     | 1.03   |
| Samsung   | MZVL2256HCHQ-00B00 | 256 GB | 1       | 373   | 0     | 1.02   |
| Phison    | PCIe SSD           | 500 GB | 7       | 370   | 0     | 1.02   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 1       | 367   | 0     | 1.01   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 1       | 367   | 0     | 1.01   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 4       | 365   | 0     | 1.00   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 3       | 364   | 0     | 1.00   |
| WDC       | PC SN520 NVMe      | 512 GB | 1       | 349   | 0     | 0.96   |
| Samsung   | PM951 NVMe         | 1 TB   | 1       | 340   | 0     | 0.93   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 5       | 339   | 0     | 0.93   |
| Corsair   | Force MP600        | 2 TB   | 2       | 336   | 0     | 0.92   |
| Silico... | 512GB PCS PCIe ... | 512 GB | 2       | 333   | 0     | 0.91   |
| Samsung   | SSD 970 PRO        | 512 GB | 12      | 327   | 0     | 0.90   |
| ADATA     | SX6000NP           | 128 GB | 2       | 325   | 0     | 0.89   |
| Hikvision | HS-SSD-C2000Pro    | 512 GB | 1       | 320   | 0     | 0.88   |
| Team      | TM8FP4512G         | 512 GB | 1       | 319   | 0     | 0.87   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 2       | 311   | 0     | 0.85   |
| Intel     | SSDPEKKW512G8      | 512 GB | 1       | 310   | 0     | 0.85   |
| PNY       | CS1031 256GB SSD   | 256 GB | 1       | 303   | 0     | 0.83   |
| Kingston  | SA2000M81000G      | 1 TB   | 7       | 314   | 145   | 0.83   |
| Samsung   | SSD 960 EVO        | 500 GB | 11      | 301   | 0     | 0.83   |
| Plextor   | PX-256M9PeY        | 256 GB | 1       | 298   | 0     | 0.82   |
| Kingston  | SA1000M8240G       | 240 GB | 1       | 298   | 0     | 0.82   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 2       | 297   | 0     | 0.81   |
| Micron    | 2200S NVMe         | 256 GB | 2       | 293   | 0     | 0.80   |
| Samsung   | SM951 NVMe         | 512 GB | 1       | 288   | 0     | 0.79   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 1       | 286   | 0     | 0.78   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 2       | 279   | 0     | 0.77   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 1       | 278   | 0     | 0.76   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 9       | 278   | 0     | 0.76   |
| Samsung   | SSD 960 EVO        | 1 TB   | 3       | 317   | 1     | 0.76   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 4       | 278   | 0     | 0.76   |
| WDC       | WDBA3V0010BNC-WRSN | 1 TB   | 1       | 276   | 0     | 0.76   |
| Micron    | MTFDHBK256TDP      |        | 1       | 275   | 0     | 0.75   |
| ADATA     | SX8200PNP          | 1 TB   | 9       | 288   | 6     | 0.75   |
| Crucial   | CT500P1SSD8        | 500 GB | 7       | 272   | 0     | 0.75   |
| Micron    | 7300_MTFDHBA400TDG | 400 GB | 2       | 272   | 0     | 0.75   |
| Samsung   | SSD 970 PRO        | 1 TB   | 8       | 271   | 0     | 0.74   |
| Samsung   | SSD 970 EVO        | 250 GB | 14      | 270   | 0     | 0.74   |
| Samsung   | PM991 NVMe         | 512 GB | 1       | 265   | 0     | 0.73   |
| Phison    | Sabrent            | 1 TB   | 18      | 264   | 0     | 0.73   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 13      | 263   | 0     | 0.72   |
| Toshiba   | THNSF5512GPUK      | 512 GB | 1       | 263   | 0     | 0.72   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 3       | 263   | 0     | 0.72   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 259   | 0     | 0.71   |
| PNY       | CS2130 1TB SSD     | 1 TB   | 1       | 256   | 0     | 0.70   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 255   | 0     | 0.70   |
| Samsung   | MZVLW256HEHP-00000 | 256 GB | 1       | 253   | 0     | 0.69   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 3       | 249   | 0     | 0.68   |
| Gigaby... | GP-AG42TB          | 2 TB   | 2       | 249   | 0     | 0.68   |
| ADATA     | SX8200PNP          | 512 GB | 6       | 305   | 1     | 0.67   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 2       | 240   | 0     | 0.66   |
| minisf... | 512GB              | 512 GB | 2       | 239   | 0     | 0.66   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 7       | 239   | 0     | 0.66   |
| Intel     | SSDPEKNW512G8      | 512 GB | 9       | 237   | 0     | 0.65   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 2       | 236   | 0     | 0.65   |
| Intel     | MEMPEK1J016GAD     | 16 GB  | 1       | 235   | 0     | 0.65   |
| Phison    | Sabrent Rocket 4.0 | 2 TB   | 1       | 233   | 0     | 0.64   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 26      | 231   | 0     | 0.64   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 14      | 230   | 0     | 0.63   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 1       | 225   | 0     | 0.62   |
| Corsair   | Force MP510        | 480 GB | 2       | 224   | 0     | 0.62   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 4       | 221   | 0     | 0.61   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 10      | 219   | 0     | 0.60   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 1       | 218   | 0     | 0.60   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 218   | 0     | 0.60   |
| Silico... | R5MP240G8          | 240 GB | 1       | 218   | 0     | 0.60   |
| Kingston  | SA2000M8500G       | 500 GB | 10      | 217   | 0     | 0.60   |
| Silico... | Asgard AN2 500N... | 500 GB | 1       | 216   | 0     | 0.59   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 2       | 216   | 0     | 0.59   |
| Transcend | TS500GMTE240S      | 500 GB | 2       | 214   | 0     | 0.59   |
| PNY       | CS3030 500GB SSD   | 500 GB | 3       | 212   | 0     | 0.58   |
| Corsair   | Force MP510        | 240 GB | 4       | 209   | 0     | 0.57   |
| Phison    | Viper M.2 VPN100   | 256 GB | 1       | 208   | 0     | 0.57   |
| Samsung   | MZVLB1T0HALR-000L2 | 1 TB   | 1       | 208   | 0     | 0.57   |
| Samsung   | PM9A1 NVMe         | 256 GB | 1       | 208   | 0     | 0.57   |
| Kingston  | RBUSNS8154P3256GJ  | 256 GB | 1       | 207   | 0     | 0.57   |
| KIOXIA    | KBG40ZPZ512G NVMe  | 512 GB | 1       | 207   | 0     | 0.57   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 2       | 203   | 0     | 0.56   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 3       | 200   | 0     | 0.55   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 5       | 198   | 0     | 0.54   |
| Mushkin   | MKNSSDPE500GB-D8   | 500 GB | 1       | 195   | 0     | 0.54   |
| Seagate   | IronWolf ZP500N... | 500 GB | 1       | 195   | 0     | 0.53   |
| Intel     | HBRPEKNX0101AH     | 256 GB | 2       | 192   | 0     | 0.53   |
| Silico... | 512GB              | 512 GB | 2       | 188   | 0     | 0.52   |
| Toshiba   | KXG50PNV2T04 NVMe  | 2 TB   | 1       | 188   | 0     | 0.52   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 6       | 186   | 0     | 0.51   |
| WDC       | PC SN730 NVMe      | 1 TB   | 2       | 183   | 0     | 0.50   |
| SSSTC     | CL1-4D256          | 256 GB | 2       | 182   | 0     | 0.50   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 182   | 0     | 0.50   |
| ADATA     | SX8200PNP          | 2 TB   | 1       | 181   | 0     | 0.50   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 4       | 176   | 0     | 0.48   |
| Samsung   | PM951 NVMe         | 256 GB | 3       | 176   | 0     | 0.48   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 8       | 204   | 1     | 0.48   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 6       | 174   | 0     | 0.48   |
| Corsair   | Force MP300        | 120 GB | 1       | 173   | 0     | 0.47   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 1       | 172   | 0     | 0.47   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 1       | 172   | 0     | 0.47   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 1       | 171   | 0     | 0.47   |
| Toshiba   | KBG30ZMV512G       | 512 GB | 1       | 171   | 0     | 0.47   |
| Samsung   | SSD 960 PRO        | 2 TB   | 1       | 170   | 0     | 0.47   |
| SK hynix  | BC511 NVMe         | 256 GB | 1       | 170   | 0     | 0.47   |
| Kingston  | SA1000M8480G       | 480 GB | 1       | 170   | 0     | 0.47   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 1       | 169   | 0     | 0.46   |
| Intel     | SSDPEDMW800G4      | 800 GB | 1       | 168   | 0     | 0.46   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 13      | 181   | 15    | 0.46   |
| Toshiba   | RD400              | 256 GB | 1       | 167   | 0     | 0.46   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 3       | 167   | 0     | 0.46   |
| Samsung   | MZVLQ512HBLU-00B00 | 512 GB | 1       | 166   | 0     | 0.46   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 166   | 0     | 0.46   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 12      | 165   | 0     | 0.45   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 1       | 164   | 0     | 0.45   |
| Kingston  | SKC2500M8500G      | 500 GB | 1       | 163   | 0     | 0.45   |
| ADATA     | SX8200PNP          | 256 GB | 6       | 162   | 0     | 0.44   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 161   | 0     | 0.44   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 30      | 161   | 0     | 0.44   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 5       | 160   | 0     | 0.44   |
| Goodram   | SSDPR-PX500-256-80 | 256 GB | 3       | 160   | 0     | 0.44   |
| SK hynix  | PC300 NVMe         | 256 GB | 1       | 159   | 0     | 0.44   |
| Acer      | SSD FA100          | 256 GB | 1       | 156   | 0     | 0.43   |
| HP        | SSD EX950          | 2 TB   | 1       | 156   | 0     | 0.43   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 2       | 154   | 0     | 0.42   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 2       | 154   | 0     | 0.42   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 3       | 152   | 0     | 0.42   |
| Toshiba   | RC100              | 240 GB | 1       | 151   | 0     | 0.41   |
| Corsair   | Force MP600        | 1 TB   | 1       | 151   | 0     | 0.41   |
| ORICO     | V500               | 1 TB   | 1       | 149   | 0     | 0.41   |
| SK hynix  | SHGP31-500GM-2     | 500 GB | 5       | 147   | 0     | 0.40   |
| KIOXIA    | KBG40ZNS128G NVMe  | 128 GB | 2       | 147   | 0     | 0.40   |
| Gigabyte  | GP-GSM2NE3256GNTD  |        | 6       | 147   | 0     | 0.40   |
| Toshiba   | KBG40ZNT512G ME... | 512 GB | 2       | 147   | 0     | 0.40   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 4       | 144   | 0     | 0.39   |
| Toshiba   | THNSF5256GCJ7      | 256 GB | 1       | 142   | 0     | 0.39   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 4       | 141   | 0     | 0.39   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 6       | 141   | 0     | 0.39   |
| KIOXIA    | KBG40ZNV1T02       | 1 TB   | 1       | 140   | 0     | 0.39   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 2       | 140   | 0     | 0.39   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 6       | 140   | 0     | 0.38   |
| Transcend | TS128GMTE110S      | 128 GB | 11      | 139   | 0     | 0.38   |
| Samsung   | MZFLV256HCHP-000MV | 256 GB | 1       | 138   | 0     | 0.38   |
| Lumino... | NVME               | 512 GB | 1       | 137   | 0     | 0.38   |
| ADATA     | IM2P33F8BR1-512GB  | 512 GB | 1       | 137   | 0     | 0.38   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 6       | 137   | 0     | 0.38   |
| WDC       | PC SN520 NVMe      | 256 GB | 2       | 136   | 0     | 0.37   |
| Silico... | NE-256             | 256 GB | 5       | 135   | 0     | 0.37   |
| Samsung   | SSD 970 EVO        | 500 GB | 23      | 153   | 1     | 0.37   |
| LDLC      | F8+M.2 240         | 240 GB | 2       | 134   | 0     | 0.37   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 7       | 134   | 0     | 0.37   |
| Toshiba   | KBG40ZNS256G NVMe  | 256 GB | 1       | 133   | 0     | 0.37   |
| Silico... | GV256              | 256 GB | 1       | 133   | 0     | 0.37   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 5       | 132   | 0     | 0.36   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 10      | 132   | 0     | 0.36   |
| WDC       | WDBRPG0010BNC-WRSN | 1 TB   | 2       | 131   | 0     | 0.36   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 6       | 130   | 0     | 0.36   |
| Micron    | 2450_MTFDKBA512TFK | 512 GB | 1       | 130   | 0     | 0.36   |
| Kingston  | SA2000M8250G       | 250 GB | 10      | 129   | 0     | 0.36   |
| SK hynix  | BC501 NVMe         | 256 GB | 1       | 129   | 0     | 0.35   |
| Samsung   | PM981 NVMe         | 256 GB | 4       | 127   | 0     | 0.35   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 11      | 127   | 0     | 0.35   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 2       | 126   | 0     | 0.35   |
| ADATA     | SX8200NP           | 480 GB | 1       | 124   | 0     | 0.34   |
| Samsung   | MZVLW512HMJP-000L7 | 512 GB | 1       | 124   | 0     | 0.34   |
| Intel     | SSDPEL1K100GA      | 100 GB | 1       | 123   | 0     | 0.34   |
| Phison    | E12-256G-PHISON... | 256 GB | 1       | 121   | 0     | 0.33   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 7       | 120   | 0     | 0.33   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 1       | 119   | 0     | 0.33   |
| Samsung   | SSD 970 EVO        | 1 TB   | 15      | 118   | 0     | 0.33   |
| SK hynix  | PC801 NVMe         | 2 TB   | 1       | 117   | 0     | 0.32   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 1       | 117   | 0     | 0.32   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 2       | 116   | 0     | 0.32   |
| Samsung   | PM961 NVMe         | 512 GB | 1       | 116   | 0     | 0.32   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 1       | 115   | 0     | 0.32   |
| WDC       | WDS100T1X0E-00AFY0 | 1 TB   | 4       | 114   | 0     | 0.31   |
| Micron    | 2210_MTFDHBA512QFD | 512 GB | 1       | 113   | 0     | 0.31   |
| Micron    | 2300_MTFDHBA512TDV | 512 GB | 2       | 113   | 0     | 0.31   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 3       | 112   | 0     | 0.31   |
| Samsung   | MZVLB256HBHQ-000L2 | 256 GB | 1       | 112   | 0     | 0.31   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 1       | 111   | 0     | 0.30   |
| Samsung   | SSD 980 PRO        | 250 GB | 9       | 111   | 0     | 0.30   |
| Timetec   | 35TTFP6PCIE-256G   | 256 GB | 1       | 110   | 0     | 0.30   |
| Kingston  | OM8PCP3512F-AI1    | 512 GB | 2       | 110   | 0     | 0.30   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 10      | 110   | 0     | 0.30   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 1       | 109   | 0     | 0.30   |
| Intel     | SSDPEKKW512G7      | 512 GB | 2       | 174   | 1     | 0.30   |
| MSI       | M450               | 500 GB | 1       | 109   | 0     | 0.30   |
| HP        | SSD EX920          | 256 GB | 1       | 108   | 0     | 0.30   |
| SK hynix  | BC711 NVMe         | 512 GB | 1       | 108   | 0     | 0.30   |
| T-FORCE   | TM8FP7001T         | 1 TB   | 1       | 107   | 0     | 0.29   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 41      | 106   | 0     | 0.29   |
| ASint     | AS806              | 128 GB | 1       | 106   | 0     | 0.29   |
| Samsung   | SSD 970 EVO        | 2 TB   | 2       | 364   | 130   | 0.28   |
| Seagate   | FireCuda 520 SS... | 500 GB | 6       | 103   | 0     | 0.28   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 1       | 102   | 0     | 0.28   |
| WDC       | WDS200T1XHE-00AFY0 | 2 TB   | 1       | 102   | 0     | 0.28   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 9       | 102   | 0     | 0.28   |
| HP        | SSD EX950          | 512 GB | 10      | 102   | 0     | 0.28   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 5       | 101   | 0     | 0.28   |
| Samsung   | SSD 960 PRO        | 512 GB | 4       | 173   | 1     | 0.27   |
| SK hynix  | BC511 HFM256GDJ... | 256 GB | 5       | 99    | 0     | 0.27   |
| Samsung   | PM991 NVMe         | 256 GB | 4       | 98    | 0     | 0.27   |
| Kingston  | RBUSNS8154P3256GJ3 | 256 GB | 2       | 98    | 0     | 0.27   |
| Gigabyte  | GP-GSM2NE8256GNTD  | 256 GB | 1       | 98    | 0     | 0.27   |
| Crucial   | CT2000P2SSD8       | 2 TB   | 3       | 97    | 0     | 0.27   |
| Toshiba   | KBG30ZMS256G NVMe  | 256 GB | 1       | 96    | 0     | 0.27   |
| Samsung   | 980 PRO with He... | 1 TB   | 1       | 96    | 0     | 0.27   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 1       | 96    | 0     | 0.26   |
| Samsung   | MZVLW512HMJP-000H7 | 512 GB | 1       | 96    | 0     | 0.26   |
| Micron    | 2200S NVMe         | 1 TB   | 3       | 92    | 0     | 0.25   |
| ADATA     | SX6000LNP          | 128 GB | 2       | 91    | 0     | 0.25   |
| WDC       | WDS200T2B0C-00PXH0 | 2 TB   | 1       | 91    | 0     | 0.25   |
| Transcend | TS2TMTE220S        | 2 TB   | 2       | 90    | 0     | 0.25   |
| Silico... | M Series NVMe S... | 128 GB | 1       | 89    | 0     | 0.25   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 1       | 89    | 0     | 0.24   |
| SSSTC     | CL1-8D256-HP       | 256 GB | 1       | 88    | 0     | 0.24   |
| Silico... | 128GB              | 128 GB | 2       | 83    | 0     | 0.23   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 1       | 83    | 0     | 0.23   |
| SK hynix  | SHGP31-1000GM      | 1 TB   | 2       | 81    | 0     | 0.22   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 7       | 78    | 0     | 0.21   |
| SK hynix  | BC711 NVMe         | 256 GB | 1       | 78    | 0     | 0.21   |
| Kimtigo   | SSD                | 256 GB | 1       | 77    | 0     | 0.21   |
| KIOXIA    | KXG60ZNV256G       | 256 GB | 1       | 76    | 0     | 0.21   |
| Kingston  | SNVSE500G          | 500 GB | 1       | 76    | 0     | 0.21   |
| Corsair   | Force MP600        | 500 GB | 2       | 75    | 0     | 0.21   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 2       | 74    | 0     | 0.20   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 2       | 74    | 0     | 0.20   |
| ATP       | NVMe M.2 2280 SSD  | 240 GB | 6       | 73    | 0     | 0.20   |
| Samsung   | MZVLW128HEGR-000L2 | 128 GB | 1       | 72    | 0     | 0.20   |
| Samsung   | MZALQ256HBJD-00BL2 | 256 GB | 2       | 72    | 0     | 0.20   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 1       | 71    | 0     | 0.20   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 3       | 71    | 0     | 0.20   |
| Corsair   | MP600 CORE         | 2 TB   | 1       | 71    | 0     | 0.20   |
| Kingston  | SNVS1000G          | 1 TB   | 2       | 70    | 0     | 0.19   |
| SSSTC     | CL1-3D128-Q11 NVMe | 128 GB | 1       | 70    | 0     | 0.19   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 5       | 69    | 0     | 0.19   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 2       | 69    | 0     | 0.19   |
| SK hynix  | PC711 NVMe         | 256 GB | 1       | 68    | 0     | 0.19   |
| Lenovo    | LENSE30512GMSP3... | 512 GB | 2       | 67    | 0     | 0.18   |
| Seagate   | FireCuda 520 SS... | 2 TB   | 1       | 67    | 0     | 0.18   |
| Netac     | NVMe SSD           | 512 GB | 1       | 67    | 0     | 0.18   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 1       | 66    | 0     | 0.18   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 2       | 66    | 0     | 0.18   |
| Kingston  | OM8PDP3256B-A01    | 256 GB | 6       | 66    | 0     | 0.18   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 9       | 66    | 0     | 0.18   |
| Samsung   | PM961 NVMe         | 256 GB | 2       | 65    | 0     | 0.18   |
| Samsung   | MZVLB512HBJQ-000H1 | 512 GB | 2       | 64    | 0     | 0.18   |
| Fanxiang  | S501               | 256 GB | 1       | 64    | 0     | 0.18   |
| Silico... | ASint AS806        | 128 GB | 1       | 63    | 0     | 0.18   |
| T-FORCE   | TM8FP8002T         | 2 TB   | 1       | 62    | 0     | 0.17   |
| ORTIAL    | SSD                | 128 GB | 2       | 62    | 0     | 0.17   |
| Transcend | TS256GMTE220S      | 256 GB | 1       | 60    | 0     | 0.17   |
| SK hynix  | PC611 NVMe         | 512 GB | 1       | 60    | 0     | 0.17   |
| ADATA     | SX6000PNP          | 512 GB | 1       | 59    | 0     | 0.16   |
| YMTC      | PC005              | 512 GB | 1       | 58    | 0     | 0.16   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 1       | 57    | 0     | 0.16   |
| Apple     | SSD SM0256L        | 256 GB | 1       | 57    | 0     | 0.16   |
| UMIS      | RPJTJ256MED1OWX    | 256 GB | 1       | 57    | 0     | 0.16   |
| Crucial   | CT500P5SSD8        | 500 GB | 4       | 57    | 0     | 0.16   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 1       | 57    | 0     | 0.16   |
| Star D... | PCIe SSD           | 960 GB | 2       | 55    | 0     | 0.15   |
| SanDisk   | WD_BLACK SN770     | 500 GB | 3       | 55    | 0     | 0.15   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 1       | 55    | 0     | 0.15   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 1       | 55    | 0     | 0.15   |
| Samsung   | MZALQ512HALU-000L2 | 512 GB | 2       | 54    | 0     | 0.15   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 3       | 54    | 0     | 0.15   |
| Samsung   | SSD 980            | 250 GB | 8       | 54    | 0     | 0.15   |
| Kingston  | OM8PDP3256B-AI1    | 256 GB | 2       | 54    | 0     | 0.15   |
| Gigaby... | GP-ASM2NE6100TTTD  | 1 TB   | 1       | 53    | 0     | 0.15   |
| Seagate   | BarraCuda Q5 ZP... | 500 GB | 2       | 53    | 0     | 0.15   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 1       | 52    | 0     | 0.14   |
| Samsung   | MZVL2512HCJQ-00B00 | 512 GB | 1       | 52    | 0     | 0.14   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 2       | 51    | 0     | 0.14   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 4       | 51    | 0     | 0.14   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 3       | 50    | 0     | 0.14   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 3       | 49    | 0     | 0.14   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 1       | 49    | 0     | 0.14   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 7       | 49    | 0     | 0.14   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 1       | 48    | 0     | 0.13   |
| Samsung   | MZVLQ256HAJD-000H1 | 256 GB | 3       | 48    | 0     | 0.13   |
| SanDisk   | Ultra 3D NVMe      | 500 GB | 1       | 48    | 0     | 0.13   |
| Crucial   | CT500P2SSD8        | 500 GB | 13      | 47    | 0     | 0.13   |
| Union ... | UMIS LENSE40256... | 256 GB | 2       | 47    | 0     | 0.13   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 1       | 46    | 0     | 0.13   |
| Lexar     | SSD                | 256 GB | 2       | 46    | 0     | 0.13   |
| Samsung   | MZVLB512HAJQ-000L2 | 512 GB | 1       | 45    | 0     | 0.13   |
| Samsung   | SSD 980 PRO        | 500 GB | 18      | 45    | 0     | 0.13   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 3       | 44    | 0     | 0.12   |
| Crucial   | CT250P2SSD8        | 250 GB | 13      | 44    | 0     | 0.12   |
| Micron    | 2200S NVMe         | 512 GB | 3       | 43    | 0     | 0.12   |
| KIOXIA... | SSD                | 500 GB | 3       | 43    | 0     | 0.12   |
| Samsung   | SSD 980 PRO        | 1 TB   | 22      | 42    | 0     | 0.12   |
| Kingston  | SNVS500G           | 500 GB | 7       | 42    | 0     | 0.12   |
| KIOXIA    | KXG60ZNV256G NVMe  | 256 GB | 1       | 41    | 0     | 0.11   |
| Samsung   | MZVLB2T0HMLB-00000 | 2 TB   | 1       | 41    | 0     | 0.11   |
| KIOXIA    | KXG70ZNV512G NVMe  | 512 GB | 1       | 40    | 0     | 0.11   |
| Samsung   | MZVLB512HBJQ-00A00 | 512 GB | 1       | 40    | 0     | 0.11   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 2       | 39    | 0     | 0.11   |
| Kingston  | OM8PCP3512F-AA     | 512 GB | 2       | 39    | 0     | 0.11   |
| FORESEE   | P900F128GH         | 128 GB | 1       | 39    | 0     | 0.11   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 1       | 37    | 0     | 0.10   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 2       | 36    | 0     | 0.10   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 4       | 36    | 0     | 0.10   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 1       | 36    | 0     | 0.10   |
| Kingston  | OM8PDP3512B-A01    | 512 GB | 7       | 36    | 0     | 0.10   |
| Crucial   | CT2000P5SSD8       | 2 TB   | 1       | 36    | 0     | 0.10   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 1       | 36    | 0     | 0.10   |
| Lexar     | 256GB SSD          | 256 GB | 5       | 35    | 0     | 0.10   |
| HP        | SSD EX900          | 500 GB | 2       | 35    | 0     | 0.10   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 1       | 35    | 0     | 0.10   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 2       | 34    | 0     | 0.10   |
| Enmotus   | P200-1600-128      | 1.5 TB | 1       | 34    | 0     | 0.09   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 1       | 33    | 0     | 0.09   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 6       | 33    | 0     | 0.09   |
| Samsung   | PM9A1 NVMe         | 512 GB | 5       | 33    | 0     | 0.09   |
| Lite-On   | CA3-8D512          | 512 GB | 2       | 33    | 0     | 0.09   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 7       | 32    | 0     | 0.09   |
| Phison    | SWG256G-112HI      | 256 GB | 1       | 32    | 0     | 0.09   |
| SanDisk   | WD Red SN700       | 4 TB   | 1       | 31    | 0     | 0.09   |
| Crucial   | CT500P5PSSD8       | 500 GB | 1       | 31    | 0     | 0.09   |
| Fanxiang  | S500PRO            | 256 GB | 4       | 30    | 0     | 0.08   |
| Samsung   | MZVLB256HAHQ-000L2 | 256 GB | 1       | 30    | 0     | 0.08   |
| Seagate   | BarraCuda 510 S... | 512 GB | 1       | 29    | 0     | 0.08   |
| Gigaby... | GP-GSM2NE3256GNTD  | 256 GB | 3       | 29    | 0     | 0.08   |
| Phison    | minisforum         | 512 GB | 2       | 28    | 0     | 0.08   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 1       | 28    | 0     | 0.08   |
| Samsung   | MZALQ128HBHQ-000L1 | 128 GB | 5       | 28    | 0     | 0.08   |
| KIOXIA    | KBG5AZNV1T02 LA    | 1 TB   | 1       | 26    | 0     | 0.07   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 3       | 26    | 0     | 0.07   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 5       | 26    | 0     | 0.07   |
| Intel     | SSDPEK1A118GA      | 118 GB | 1       | 26    | 0     | 0.07   |
| Silico... | GV512              | 512 GB | 1       | 26    | 0     | 0.07   |
| Patriot   | M.2 P300           | 256 GB | 3       | 25    | 0     | 0.07   |
| Samsung   | MZVLQ1T0HALB-00000 | 1 TB   | 1       | 25    | 0     | 0.07   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 1       | 25    | 0     | 0.07   |
| SanDisk   | WD Blue SN570      | 500 GB | 5       | 24    | 0     | 0.07   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 4       | 24    | 0     | 0.07   |
| Samsung   | MZVLQ512HALU-000H1 | 512 GB | 1       | 24    | 0     | 0.07   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 3       | 24    | 0     | 0.07   |
| Phison    | Sabrent Rocket ... | 512 GB | 1       | 24    | 0     | 0.07   |
| Micron    | MTFDHBA512TCK      | 512 GB | 1       | 23    | 0     | 0.07   |
| Silico... | NVME SSD           | 128 GB | 1       | 23    | 0     | 0.07   |
| Samsung   | SSD 980            | 500 GB | 15      | 37    | 3     | 0.06   |
| Kingston  | RBUSNS8154P3256GJ2 | 256 GB | 1       | 23    | 0     | 0.06   |
| Fanxiang  | S500               | 256 GB | 2       | 23    | 0     | 0.06   |
| Gigaby... | GP-GSM2NE3100TNTD  | 1 TB   | 2       | 22    | 0     | 0.06   |
| Team      | TM8FP6256G         | 256 GB | 4       | 22    | 0     | 0.06   |
| Hikvision | HS-SSD-E3000 256G  | 256 GB | 1       | 22    | 0     | 0.06   |
| Micron    | MTFDHBA512QFD-1... | 512 GB | 1       | 22    | 0     | 0.06   |
| ADATA     | IM2P33F8BR2-512GB  | 512 GB | 1       | 22    | 0     | 0.06   |
| Colorful  | CN600              | 512 GB | 1       | 22    | 0     | 0.06   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 2       | 22    | 0     | 0.06   |
| SK hynix  | PC401 NVMe         | 256 GB | 1       | 22    | 0     | 0.06   |
| ADATA     | IM2P33F8BR2-256GB  | 256 GB | 1       | 22    | 0     | 0.06   |
| Kingston  | SKC2500M8250G      | 250 GB | 2       | 22    | 0     | 0.06   |
| SK hynix  | BC511 NVMe         | 512 GB | 2       | 21    | 0     | 0.06   |
| V-GeN     | V-GEN06SM21AR51... | 512 GB | 1       | 21    | 0     | 0.06   |
| Kingston  | OM8PDP3256B-AA1    | 256 GB | 1       | 21    | 0     | 0.06   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 2       | 20    | 0     | 0.06   |
| Samsung   | SSD 980            | 1 TB   | 14      | 20    | 0     | 0.06   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 2       | 19    | 0     | 0.05   |
| Samsung   | MZVLQ256HBJD-00B   | 256 GB | 1       | 19    | 0     | 0.05   |
| Lexar     | 512GB SSD          | 512 GB | 1       | 18    | 0     | 0.05   |
| Gigaby... | GP-GSM2NE3128GNTD  | 128 GB | 1       | 18    | 0     | 0.05   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 3       | 18    | 0     | 0.05   |
| Kingston  | SNVS250G           | 250 GB | 5       | 18    | 0     | 0.05   |
| KIOXIA    | KXG60ZNV512G NVMe  | 512 GB | 1       | 16    | 0     | 0.05   |
| SK hynix  | BC511 HFM512GDJ... | 512 GB | 1       | 16    | 0     | 0.05   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 16    | 0     | 0.05   |
| WDC       | PC SN530 SDBPMP... | 512 GB | 1       | 16    | 0     | 0.04   |
| SanDisk   | WD Blue SN570      | 1 TB   | 3       | 15    | 0     | 0.04   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 1       | 15    | 0     | 0.04   |
| SK hynix  | SKHynix_HFM128G... | 128 GB | 1       | 15    | 0     | 0.04   |
| Toshiba   | KXG6APNV2T04       | 2 TB   | 1       | 15    | 0     | 0.04   |
| SK hynix  | HFM128GDJTNG-8310A | 128 GB | 1       | 14    | 0     | 0.04   |
| Hikvision | HS-SSD-C2000ECO... | 1 TB   | 1       | 14    | 0     | 0.04   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 2       | 14    | 0     | 0.04   |
| ADATA     | SX6000PNP          | 256 GB | 1       | 14    | 0     | 0.04   |
| Samsung   | MZVL2512HCJQ-00B07 | 512 GB | 4       | 14    | 0     | 0.04   |
| Toshiba   | KBG30ZPZ128G       | 128 GB | 1       | 14    | 0     | 0.04   |
| Phison    | Sabrent Rocket ... | 1 TB   | 1       | 14    | 0     | 0.04   |
| Seagate   | BarraCuda 510 S... | 250 GB | 1       | 14    | 0     | 0.04   |
| Kimtigo   | SSD                | 128 GB | 2       | 13    | 0     | 0.04   |
| ADATA     | SX6000PNP          | 1 TB   | 1       | 13    | 0     | 0.04   |
| SK hynix  | PC300 NVMe         | 512 GB | 1       | 13    | 0     | 0.04   |
| Kingston  | SKC3000S512G       | 512 GB | 1       | 12    | 0     | 0.03   |
| AGI       | AGI512G16AI198     | 512 GB | 2       | 33    | 1     | 0.03   |
| Transcend | TS256GMTE652T2     | 256 GB | 16      | 11    | 0     | 0.03   |
| SanDisk   | WD Blue SN570      | 250 GB | 3       | 11    | 0     | 0.03   |
| ADATA     | SX6000LNP          | 512 GB | 3       | 11    | 0     | 0.03   |
| Gigabyte  | GP-GSM2NE3128GNTD  | 128 GB | 2       | 11    | 0     | 0.03   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 10    | 0     | 0.03   |
| SK hynix  | PC300 HFS512GD9... | 512 GB | 1       | 10    | 0     | 0.03   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 2       | 10    | 0     | 0.03   |
| Samsung   | PM981a NVMe        | 512 GB | 1       | 10    | 0     | 0.03   |
| Nfortec   | ALCYON             | 256 GB | 1       | 10    | 0     | 0.03   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 1       | 10    | 0     | 0.03   |
| SK hynix  | HFM512GD3JX013N    | 512 GB | 1       | 10    | 0     | 0.03   |
| Phison    | 311CD0512GB        | 512 GB | 1       | 9     | 0     | 0.03   |
| Samsung   | MZALQ256HAJD-000L2 | 256 GB | 3       | 9     | 0     | 0.03   |
| WDC       | PC SN530 NVMe      | 512 GB | 1       | 9     | 0     | 0.02   |
| WDC       | PC SN730 NVMe      | 512 GB | 1       | 8     | 0     | 0.02   |
| Mushkin   | MKNSSDHL500GB-D8   | 500 GB | 2       | 8     | 0     | 0.02   |
| BIWIN     | SSD                | 1 TB   | 2       | 8     | 0     | 0.02   |
| Lite-On   | CL1-8D256          | 256 GB | 1       | 8     | 0     | 0.02   |
| SanDisk   | WD_BLACK SN850     | 1 TB   | 2       | 7     | 0     | 0.02   |
| Crucial   | CT500P3SSD8        | 500 GB | 2       | 7     | 0     | 0.02   |
| Intel     | SSDPEKNU512GZ      | 512 GB | 2       | 7     | 0     | 0.02   |
| WDC       | PC SN530 NVMe      | 256 GB | 2       | 7     | 0     | 0.02   |
| FORESEE   | P900F128GBH        | 128 GB | 1       | 7     | 0     | 0.02   |
| KingFast  | 128GB              | 128 GB | 1       | 6     | 0     | 0.02   |
| Union ... | UMIS LENSE40512... | 512 GB | 1       | 6     | 0     | 0.02   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 3       | 6     | 0     | 0.02   |
| Kingston  | SKC3000S1024G      | 1 TB   | 4       | 6     | 0     | 0.02   |
| ADATA     | FALCON             | 256 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | SNV2S500G          | 500 GB | 1       | 6     | 0     | 0.02   |
| Micron    | MTFDKBA512TFH-1... | 512 GB | 1       | 6     | 0     | 0.02   |
| Silico... | Aura Pro X2        | 960 GB | 1       | 6     | 0     | 0.02   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 2       | 6     | 0     | 0.02   |
| Kingston  | RBUSNS8154P3256GJ1 | 256 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 1       | 6     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 2       | 5     | 0     | 0.02   |
| Samsung   | SSD 980 PRO wit... | 1 TB   | 1       | 5     | 0     | 0.02   |
| SanDisk   | WD Blue SN570 5... | 500 GB | 1       | 5     | 0     | 0.01   |
| Toshiba   | KBG30ZMV256G KI... | 256 GB | 1       | 5     | 0     | 0.01   |
| WDC       | WDS500G1X0E-00AFY0 | 500 GB | 3       | 5     | 0     | 0.01   |
| CWDISK    | 128GB              | 128 GB | 1       | 5     | 0     | 0.01   |
| Micron    | 2300 NVMe          | 512 GB | 2       | 5     | 0     | 0.01   |
| KIOXIA    | KXG60PNV2T04 NVMe  | 2 TB   | 1       | 4     | 0     | 0.01   |
| Samsung   | SSD 980 PRO        | 2 TB   | 5       | 4     | 0     | 0.01   |
| Samsung   | MZALQ512HBLU-00BL2 | 512 GB | 3       | 4     | 0     | 0.01   |
| Patriot   | M.2 P300           | 128 GB | 1       | 4     | 0     | 0.01   |
| Phison    | ESO512GYLCT-EP3-2L | 512 GB | 1       | 4     | 0     | 0.01   |
| Fanxiang  | S501               | 512 GB | 1       | 4     | 0     | 0.01   |
| Kingston  | OM8PCP3512F-AB1    | 512 GB | 1       | 3     | 0     | 0.01   |
| SSSTC     | CL1-4D128          | 128 GB | 1       | 3     | 0     | 0.01   |
| SK hynix  | HFM256GDHTNG-8510B | 256 GB | 1       | 3     | 0     | 0.01   |
| UMIS      | RPJTJ128MEE1MWX    | 128 GB | 1       | 3     | 0     | 0.01   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 1       | 3     | 0     | 0.01   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 1       | 3     | 0     | 0.01   |
| SSSTC     | CL1-8D256          | 256 GB | 1       | 3     | 0     | 0.01   |
| Samsung   | MZALQ128HBHQ-000L2 | 128 GB | 1       | 3     | 0     | 0.01   |
| Silico... | GV128              | 128 GB | 3       | 3     | 0     | 0.01   |
| Silico... | 512GB MEGA S3      | 512 GB | 1       | 3     | 0     | 0.01   |
| Samsung   | MZVL21T0HCLR-00BL7 | 1 TB   | 3       | 3     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 2       | 3     | 0     | 0.01   |
| Intel     | 670p SSDPEKNU51... | 512 GB | 1       | 2     | 0     | 0.01   |
| Phison    | APS-SE20G-256      | 256 GB | 1       | 2     | 0     | 0.01   |
| Team      | TM8FP6512G         | 512 GB | 1       | 2     | 0     | 0.01   |
| Crucial   | CT500P3PSSD8       | 500 GB | 1       | 2     | 0     | 0.01   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 1       | 2     | 0     | 0.01   |
| Kingston  | SFYRS1000G         | 1 TB   | 1       | 2     | 0     | 0.01   |
| Micron    | MTFDHBA512TDV      | 512 GB | 1       | 2     | 0     | 0.01   |
| UMIS      | RPJTJ256MEE1OWX    | 256 GB | 1       | 2     | 0     | 0.01   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 1       | 2     | 0     | 0.01   |
| Mushkin   | MKNSSDHL1TB-D8     | 1 TB   | 1       | 2     | 0     | 0.01   |
| Crucial   | CT1000P3SSD8       | 1 TB   | 1       | 2     | 0     | 0.01   |
| KIOXIA    | KBG50ZNV512G       | 512 GB | 1       | 2     | 0     | 0.01   |
| Phison    | E12S-512G-PHISO... | 512 GB | 1       | 2     | 0     | 0.01   |
| LDLC      | F8+M.2 480         | 480 GB | 1       | 2     | 0     | 0.01   |
| Micron    | 2450_MTFDKBA1T0TFK | 1 TB   | 1       | 2     | 0     | 0.01   |
| Samsung   | 980 PRO with He... | 2 TB   | 1       | 2     | 0     | 0.01   |
| WDC       | WDS240G2G0C-00AJM0 | 240 GB | 1       | 1     | 0     | 0.01   |
| FORESEE   | XP1000F001T        | 1 TB   | 2       | 1     | 0     | 0.01   |
| Kingston  | OM8SBP3512K-AH     | 512 GB | 1       | 1     | 0     | 0.01   |
| BR        | 128GB              | 128 GB | 1       | 1     | 0     | 0.00   |
| Silico... | PCIe SSD           | 256 GB | 1       | 1     | 0     | 0.00   |
| Fanxiang  | S500               | 128 GB | 4       | 1     | 0     | 0.00   |
| UMIS      | RPFTJ128PDD2EWX    | 128 GB | 1       | 1     | 0     | 0.00   |
| Union ... | RPFTJ128PDD2EWX    | 128 GB | 1       | 1     | 0     | 0.00   |
| Pioneer   | APS-SE10N-256      | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 1       | 1     | 0     | 0.00   |
| ShiJi     | 256GB M.2-NVMe     | 256 GB | 2       | 1     | 0     | 0.00   |
| Seagate   | FireCuda 510 SS... | 500 GB | 1       | 1     | 0     | 0.00   |
| XrayDisk  | 256GB SSD          | 256 GB | 1       | 1     | 0     | 0.00   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 1       | 1     | 0     | 0.00   |
| SPCC      | M.2 PCIe SSD       | 128 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | PM981 NVMe         | 1 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Lexar     | 250GB SSD          | 250 GB | 1       | 0     | 0     | 0.00   |
| Fanxiang  | S501               | 128 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 1       | 0     | 0     | 0.00   |
| Phison    | E19-256G-PHISON... | 256 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 3       | 0     | 0     | 0.00   |
| Kingston  | OM8PCP3512F-A02    | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | PC611 NVMe         | 256 GB | 1       | 0     | 0     | 0.00   |
| AMD       | R5MP128G8          | 128 GB | 1       | 0     | 0     | 0.00   |
| Corsair   | MP600 GS           | 1 TB   | 1       | 0     | 0     | 0.00   |
| Kingston  | SNVS500GB          | 500 GB | 1       | 0     | 0     | 0.00   |
| Micron    | 3400_MTFDKBA1T0TFH | 1 TB   | 1       | 0     | 0     | 0.00   |
| KIOXIA    | KBG40ZNV256G       | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZALQ512HBLU-00BL1 | 512 GB | 4       | 0     | 0     | 0.00   |
| Solid ... | CL1-3D128-Q11 N... | 128 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | KXG60PNV2T04 NV... | 2 TB   | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFM512GDHTNG-8310A | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZALQ256HAJD-000L1 | 256 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | MZVLB512HBJQ-000   | 512 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 1       | 0     | 0     | 0.00   |
| EMTEC     | X300               | 128 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SNVS2000G          | 2 TB   | 1       | 0     | 0     | 0.00   |
| Transcend | TS1TMTE110S        | 1 TB   | 1       | 0     | 0     | 0.00   |
| Silico... | 500GB-PRO-X-SS     | 500 GB | 1       | 0     | 0     | 0.00   |
| Goodram   | SSDPR-PX500-512-80 | 512 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SNV2S250G          | 250 GB | 1       | 0     | 0     | 0.00   |

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
| Plextor     | 3      | 3       | 780   | 0     | 2.14   |
| EAGET       | 1      | 1       | 493   | 0     | 1.35   |
| Reletech    | 1      | 1       | 403   | 0     | 1.11   |
| Intel       | 37     | 91      | 302   | 1     | 0.80   |
| Toshiba     | 29     | 46      | 276   | 0     | 0.76   |
| Phison      | 18     | 51      | 249   | 0     | 0.68   |
| minisforum  | 1      | 2       | 239   | 0     | 0.66   |
| PNY         | 4      | 8       | 224   | 0     | 0.62   |
| ADATA       | 16     | 38      | 217   | 2     | 0.56   |
| HP          | 6      | 18      | 196   | 0     | 0.54   |
| Corsair     | 9      | 15      | 174   | 0     | 0.48   |
| WDC         | 64     | 180     | 171   | 0     | 0.47   |
| Acer        | 1      | 1       | 156   | 0     | 0.43   |
| Samsung     | 110    | 516     | 159   | 1     | 0.42   |
| ORICO       | 1      | 1       | 149   | 0     | 0.41   |
| Lenovo      | 3      | 5       | 144   | 0     | 0.40   |
| XPG         | 1      | 6       | 141   | 0     | 0.39   |
| LuminouTek  | 1      | 1       | 137   | 0     | 0.38   |
| SPCC        | 5      | 15      | 134   | 0     | 0.37   |
| KIOXIA      | 15     | 28      | 132   | 0     | 0.36   |
| Silicon ... | 17     | 26      | 121   | 0     | 0.33   |
| Goodram     | 2      | 4       | 120   | 0     | 0.33   |
| Hikvision   | 3      | 3       | 119   | 0     | 0.33   |
| Patriot     | 3      | 5       | 115   | 0     | 0.32   |
| SSSTC       | 6      | 9       | 114   | 0     | 0.31   |
| Kingston    | 36     | 95      | 114   | 11    | 0.31   |
| Gigabyte    | 4      | 10      | 112   | 0     | 0.31   |
| Timetec     | 1      | 1       | 110   | 0     | 0.30   |
| MSI         | 1      | 1       | 109   | 0     | 0.30   |
| Micron      | 18     | 28      | 107   | 0     | 0.29   |
| ASint       | 1      | 1       | 106   | 0     | 0.29   |
| Crucial     | 13     | 75      | 96    | 3     | 0.26   |
| Transcend   | 7      | 34      | 92    | 0     | 0.25   |
| LDLC        | 2      | 3       | 90    | 0     | 0.25   |
| T-FORCE     | 2      | 2       | 85    | 0     | 0.23   |
| SK hynix    | 36     | 57      | 82    | 0     | 0.23   |
| Gigabyte... | 5      | 9       | 78    | 0     | 0.21   |
| Seagate     | 10     | 16      | 73    | 0     | 0.20   |
| ATP         | 1      | 6       | 73    | 0     | 0.20   |
| Team        | 3      | 6       | 68    | 0     | 0.19   |
| Netac       | 1      | 1       | 67    | 0     | 0.18   |
| ORTIAL      | 1      | 2       | 62    | 0     | 0.17   |
| YMTC        | 1      | 1       | 58    | 0     | 0.16   |
| Apple       | 1      | 1       | 57    | 0     | 0.16   |
| Star Drive  | 1      | 2       | 55    | 0     | 0.15   |
| Mushkin     | 3      | 4       | 53    | 0     | 0.15   |
| KIOXIA-E... | 1      | 3       | 43    | 0     | 0.12   |
| Kimtigo     | 2      | 3       | 35    | 0     | 0.10   |
| Enmotus     | 1      | 1       | 34    | 0     | 0.09   |
| Lexar       | 4      | 9       | 32    | 0     | 0.09   |
| Union Me... | 3      | 4       | 25    | 0     | 0.07   |
| SanDisk     | 8      | 19      | 24    | 0     | 0.07   |
| Lite-On     | 2      | 3       | 24    | 0     | 0.07   |
| Colorful    | 1      | 1       | 22    | 0     | 0.06   |
| V-GeN       | 1      | 1       | 21    | 0     | 0.06   |
| Fanxiang    | 6      | 13      | 18    | 0     | 0.05   |
| UMIS        | 4      | 4       | 16    | 0     | 0.04   |
| FORESEE     | 3      | 4       | 12    | 0     | 0.03   |
| AGI         | 1      | 2       | 33    | 1     | 0.03   |
| Nfortec     | 1      | 1       | 10    | 0     | 0.03   |
| BIWIN       | 1      | 2       | 8     | 0     | 0.02   |
| KingFast    | 1      | 1       | 6     | 0     | 0.02   |
| CWDISK      | 1      | 1       | 5     | 0     | 0.01   |
| BR          | 1      | 1       | 1     | 0     | 0.00   |
| Pioneer     | 1      | 1       | 1     | 0     | 0.00   |
| ShiJi       | 1      | 2       | 1     | 0     | 0.00   |
| XrayDisk    | 1      | 1       | 1     | 0     | 0.00   |
| AMD         | 1      | 1       | 0     | 0     | 0.00   |
| Solid St... | 1      | 1       | 0     | 0     | 0.00   |
| EMTEC       | 1      | 1       | 0     | 0     | 0.00   |

