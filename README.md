HDD/SSD Reliability Test
========================

This is a project to estimate reliability of HDD/SSD drives by
the analysis of SMART data collected by BSD users at https://bsd-hardware.info. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe/blob/master/INSTALL.BSD.md) tool:

    hw-probe -all -upload

Total drives: 8463.

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

Number_Of_Important_Errors — number of important errors that can indicate a drive failure:

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

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See full list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Seagate   | ST3120023A         | 120 GB | 1       | 5214  | 0     | 14.29  |
| WDC       | WD800JD-08MSA1     | 80 GB  | 1       | 4687  | 0     | 12.84  |
| WDC       | WD1600AAJS-00PSA0  | 160 GB | 1       | 4208  | 0     | 11.53  |
| WDC       | WD1600JB-00REA0    | 160 GB | 1       | 4140  | 0     | 11.34  |
| WDC       | WD1600JD-00GBB0    | 160 GB | 4       | 5313  | 4     | 11.14  |
| WDC       | WD1602ABJS-43P5A0  | 160 GB | 1       | 4045  | 0     | 11.08  |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 3       | 3833  | 0     | 10.50  |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 1       | 3820  | 0     | 10.47  |
| WDC       | WD2500AAJS-00V4A0  | 250 GB | 1       | 3798  | 0     | 10.41  |
| Hitachi   | HDS725050KLA360    | 500 GB | 1       | 3763  | 0     | 10.31  |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 2       | 3704  | 0     | 10.15  |
| Hitachi   | HDT721032SLA360    | 320 GB | 1       | 3534  | 0     | 9.68   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 4       | 3472  | 0     | 9.51   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 1       | 3468  | 0     | 9.50   |
| WDC       | WD1600BEKT-75A25T0 | 160 GB | 1       | 3424  | 0     | 9.38   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 1       | 3387  | 0     | 9.28   |
| WDC       | WD1600AAJS-60M0A1  | 160 GB | 1       | 3365  | 0     | 9.22   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 3       | 3329  | 0     | 9.12   |
| Seagate   | ST3300831AS        | 304 GB | 1       | 3187  | 0     | 8.73   |
| Seagate   | ST3360320AS        | 360 GB | 1       | 3119  | 0     | 8.55   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 6       | 3085  | 0     | 8.45   |
| WDC       | WD1602ABKS-18N8A0  | 160 GB | 1       | 2978  | 0     | 8.16   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 3       | 2977  | 0     | 8.16   |
| WDC       | WD800EB-00DJF0     | 80 GB  | 1       | 2959  | 0     | 8.11   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 1       | 2917  | 0     | 7.99   |
| Seagate   | ST3808110AS        | 80 GB  | 2       | 2844  | 0     | 7.79   |
| Seagate   | ST3320413AS        | 320 GB | 1       | 2815  | 0     | 7.71   |
| WDC       | WD400BB-00GFA0     | 40 GB  | 1       | 2808  | 0     | 7.69   |
| Seagate   | ST3500630NS        | 500 GB | 5       | 2803  | 0     | 7.68   |
| WDC       | WD400BB-00JHC0     | 40 GB  | 1       | 2800  | 0     | 7.67   |
| Hitachi   | HUA7250SBSUN500G   | 500 GB | 2       | 2785  | 0     | 7.63   |
| Seagate   | ST500DL001 HD503HI | 500 GB | 1       | 2746  | 0     | 7.52   |
| HGST      | HUS724030ALA640    | 3 TB   | 1       | 2737  | 0     | 7.50   |
| Seagate   | ST32000645NS       | 2 TB   | 1       | 2713  | 0     | 7.43   |
| HP        | GB0500EAFYL        | 500 GB | 3       | 2702  | 0     | 7.40   |
| Hitachi   | HDT725025VLA380    | 250 GB | 1       | 2680  | 0     | 7.34   |
| WDC       | WD3200AAKX-00ERMA0 | 320 GB | 1       | 2660  | 0     | 7.29   |
| Seagate   | ST33000651NS       | 3 TB   | 1       | 2619  | 0     | 7.18   |
| Hitachi   | HUA721050KLA330    | 500 GB | 2       | 3842  | 1     | 7.02   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 3       | 2560  | 0     | 7.01   |
| Samsung   | HD502IJ            | 500 GB | 2       | 2696  | 1     | 6.93   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 1       | 2510  | 0     | 6.88   |
| WDC       | WD10EACS-65D6B0    | 1 TB   | 1       | 2509  | 0     | 6.88   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 5       | 2494  | 0     | 6.83   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 1       | 2483  | 0     | 6.81   |
| WDC       | WD2500JD-75HBB0    | 250 GB | 1       | 2439  | 0     | 6.68   |
| Seagate   | ST32000641AS       | 2 TB   | 5       | 2439  | 0     | 6.68   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 3       | 2436  | 0     | 6.67   |
| WDC       | WD1600AABS-61PRA0  | 160 GB | 1       | 2420  | 0     | 6.63   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 1       | 2414  | 0     | 6.61   |
| HP        | GB0250EAFYK        | 250 GB | 3       | 3054  | 1     | 6.61   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 5       | 3228  | 1     | 6.56   |
| Maxtor    | 6V080E0            | 82 GB  | 1       | 2371  | 0     | 6.50   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 2       | 2344  | 0     | 6.42   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 1       | 2343  | 0     | 6.42   |
| Seagate   | ST500LX003-1AC15G  | 500 GB | 1       | 2334  | 0     | 6.40   |
| WDC       | WD1003FBYX-23 0... | 1 TB   | 2       | 2317  | 0     | 6.35   |
| Seagate   | ST380011A          | 80 GB  | 2       | 2314  | 0     | 6.34   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 3       | 2281  | 0     | 6.25   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 1       | 2257  | 0     | 6.19   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 2       | 2241  | 0     | 6.14   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 1       | 2187  | 0     | 5.99   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 2168  | 0     | 5.94   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 5       | 2150  | 0     | 5.89   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 1       | 2120  | 0     | 5.81   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 3       | 2101  | 0     | 5.76   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 6       | 2302  | 1     | 5.75   |
| Hitachi   | HDS728080PLA380    | 82 GB  | 1       | 2086  | 0     | 5.72   |
| Hitachi   | HDS5C4040ALE630    | 4 TB   | 21      | 2076  | 0     | 5.69   |
| WDC       | WD3200BEKT-08PVMT1 | 320 GB | 5       | 2075  | 0     | 5.69   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 1       | 2024  | 0     | 5.55   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 3       | 2019  | 0     | 5.53   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 2       | 2009  | 0     | 5.51   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 3       | 1988  | 0     | 5.45   |
| Seagate   | ST3400633AS        | 400 GB | 1       | 1978  | 0     | 5.42   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 1       | 1968  | 0     | 5.39   |
| Seagate   | ST3500414CS        | 500 GB | 5       | 1966  | 0     | 5.39   |
| HGST      | HUS724020ALA640    | 2 TB   | 6       | 1955  | 0     | 5.36   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 1       | 1925  | 0     | 5.28   |
| WDC       | WD2000JD-00FYB0    | 200 GB | 1       | 3833  | 1     | 5.25   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 20      | 2403  | 1     | 5.24   |
| Seagate   | ST3320620A         | 320 GB | 1       | 1913  | 0     | 5.24   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 3       | 1913  | 0     | 5.24   |
| WDC       | WD360ADFD-00NLR5   | 37 GB  | 1       | 1910  | 0     | 5.23   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 18      | 2020  | 2     | 5.23   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 1       | 1894  | 0     | 5.19   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 2       | 1869  | 0     | 5.12   |
| Seagate   | ST3160215ACE       | 160 GB | 1       | 1863  | 0     | 5.11   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 1       | 1848  | 0     | 5.06   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 6       | 2134  | 2     | 5.04   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 10      | 1993  | 2     | 5.01   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 1       | 1827  | 0     | 5.01   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 1       | 1824  | 0     | 5.00   |
| HGST      | HUH728060ALE600    | 6 TB   | 1       | 1820  | 0     | 4.99   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 1       | 1819  | 0     | 4.98   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 2       | 1816  | 0     | 4.98   |
| Seagate   | ST1500DL003-9VT16L | 1.5 TB | 1       | 1816  | 0     | 4.98   |
| Seagate   | ST4000NC000-1FR168 | 4 TB   | 2       | 1810  | 0     | 4.96   |
| Hitachi   | HTE545050B9A300    | 500 GB | 1       | 1809  | 0     | 4.96   |
| Maxtor    | STM3250820A        | 250 GB | 1       | 1802  | 0     | 4.94   |
| Seagate   | ST9320421AS        | 320 GB | 1       | 1802  | 0     | 4.94   |
| Hitachi   | HTS545016B9A300    | 160 GB | 1       | 1788  | 0     | 4.90   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 2       | 3527  | 3     | 4.88   |
| Hitachi   | HTE543232A7A384    | 320 GB | 2       | 1766  | 0     | 4.84   |
| Toshiba   | MG03ACA200         | 2 TB   | 6       | 1760  | 0     | 4.82   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 4       | 1752  | 0     | 4.80   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 12      | 2044  | 104   | 4.80   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 7       | 1913  | 145   | 4.76   |
| Seagate   | ST6000DX000-1H217Z | 6 TB   | 2       | 1714  | 0     | 4.70   |
| Samsung   | HD161GJ            | 160 GB | 2       | 1709  | 0     | 4.68   |
| Samsung   | HD103SJ            | 1 TB   | 6       | 1965  | 1     | 4.63   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 32      | 1735  | 33    | 4.60   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 13      | 1778  | 156   | 4.59   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 3       | 1671  | 0     | 4.58   |
| Seagate   | ST1000LM014-1EJ... | 1 TB   | 1       | 1670  | 0     | 4.58   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 2       | 1670  | 0     | 4.58   |
| HGST      | HDN724040ALE640    | 4 TB   | 17      | 1920  | 48    | 4.57   |
| HGST      | HDN724030ALE640    | 3 TB   | 7       | 1667  | 0     | 4.57   |
| Hitachi   | HCC543216A7A380    | 160 GB | 1       | 1649  | 0     | 4.52   |
| WDC       | WD5000BEVT-00A03T0 | 500 GB | 1       | 1643  | 0     | 4.50   |
| Toshiba   | MK3276GSX -63      | 320 GB | 1       | 1634  | 0     | 4.48   |
| HGST      | HTS725050A7E635... | 500 GB | 1       | 1625  | 0     | 4.45   |
| Hitachi   | HTS725032A9A360    | 320 GB | 1       | 1622  | 0     | 4.45   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 12      | 1910  | 169   | 4.36   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 12      | 2089  | 14    | 4.35   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 4       | 1574  | 0     | 4.31   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 1       | 1566  | 0     | 4.29   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 4       | 1546  | 0     | 4.24   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 1       | 1543  | 0     | 4.23   |
| Toshiba   | MG04ACA400E        | 4 TB   | 2       | 1535  | 0     | 4.21   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 1       | 1531  | 0     | 4.20   |
| Samsung   | HD204UI            | 2 TB   | 18      | 2043  | 7     | 4.18   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 1       | 1522  | 0     | 4.17   |
| Samsung   | HD502HJ            | 500 GB | 4       | 1948  | 1     | 4.17   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 2       | 1517  | 0     | 4.16   |
| Maxtor    | 6L080J4            | 80 GB  | 3       | 2093  | 2     | 4.15   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 3       | 1514  | 0     | 4.15   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 2       | 1504  | 0     | 4.12   |
| WDC       | WD7500BMVW-11AJGS4 | 752 GB | 1       | 1500  | 0     | 4.11   |
| Seagate   | ST3500412AS        | 500 GB | 1       | 1499  | 0     | 4.11   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 3       | 3419  | 4     | 4.09   |
| HP        | MB1000GCWCV        | 1 TB   | 7       | 1962  | 4     | 4.08   |
| Seagate   | ST8000DM002-1YW112 | 8 TB   | 1       | 1475  | 0     | 4.04   |
| WDC       | WD2000FYYX         | 2 TB   | 4       | 1466  | 0     | 4.02   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 2       | 1450  | 0     | 3.97   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 2       | 1449  | 0     | 3.97   |
| WDC       | WD10PURX-64D85Y0   | 1 TB   | 1       | 1445  | 0     | 3.96   |
| WDC       | WD2500JS-75NCB2    | 250 GB | 4       | 1441  | 0     | 3.95   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 3       | 1529  | 3     | 3.92   |
| Hitachi   | HDS721050CLA360    | 500 GB | 1       | 1427  | 0     | 3.91   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 6       | 1427  | 0     | 3.91   |
| Hitachi   | HDS721075KLA330    | 752 GB | 9       | 1767  | 1     | 3.90   |
| WDC       | WD2500AAJS-07M0A0  | 250 GB | 1       | 1420  | 0     | 3.89   |
| Toshiba   | MD04ACA500         | 5 TB   | 1       | 1413  | 0     | 3.87   |
| WDC       | WD4002FYYZ-01B7CB0 | 4 TB   | 2       | 1402  | 0     | 3.84   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 4       | 2652  | 3     | 3.83   |
| WDC       | WD5002ABYS-18B1B0  | 500 GB | 2       | 2250  | 4     | 3.82   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 2       | 2462  | 14    | 3.82   |
| WDC       | WD2500AAJS-00L7A0  | 250 GB | 1       | 1391  | 0     | 3.81   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 21      | 1618  | 1     | 3.80   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 1       | 1376  | 0     | 3.77   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 4       | 1797  | 28    | 3.71   |
| Hitachi   | HTS541060G9AT00    | 64 GB  | 1       | 1351  | 0     | 3.70   |
| WDC       | WD2500AAKX-753CA1  | 250 GB | 1       | 1345  | 0     | 3.69   |
| Seagate   | ST6000DM001-1YW11C | 6 TB   | 1       | 1338  | 0     | 3.67   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 13      | 1338  | 0     | 3.67   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 8       | 1869  | 95    | 3.65   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 7       | 1439  | 288   | 3.65   |
| Seagate   | ST9250410AS        | 250 GB | 3       | 1323  | 0     | 3.63   |
| Hitachi   | HDS721032CLA362    | 320 GB | 1       | 1323  | 0     | 3.63   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 2       | 2278  | 545   | 3.62   |
| Samsung   | HD501LJ            | 500 GB | 8       | 2456  | 129   | 3.62   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 1       | 1317  | 0     | 3.61   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 3       | 1317  | 0     | 3.61   |
| WDC       | WD5000BMVV-11A1CS0 | 500 GB | 1       | 1308  | 0     | 3.59   |
| WDC       | WD1600BEVS-75RST0  | 160 GB | 1       | 1301  | 0     | 3.57   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 4       | 1301  | 0     | 3.57   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 1       | 1296  | 0     | 3.55   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 6       | 1296  | 0     | 3.55   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 2       | 1632  | 1     | 3.52   |
| Seagate   | ST9500423AS        | 500 GB | 1       | 1283  | 0     | 3.52   |
| WDC       | WD5003ABYX-88 LEN  | 500 GB | 1       | 1280  | 0     | 3.51   |
| Toshiba   | DT01ACA200         | 2 TB   | 10      | 1451  | 114   | 3.50   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 2       | 1268  | 0     | 3.48   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 5       | 1267  | 0     | 3.47   |
| Samsung   | HD502HI            | 500 GB | 2       | 1266  | 0     | 3.47   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 1       | 1266  | 0     | 3.47   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 1       | 1260  | 0     | 3.45   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 32      | 1690  | 60    | 3.41   |
| WDC       | WD3200BEKT-00A25T0 | 320 GB | 1       | 1239  | 0     | 3.40   |
| HGST      | HUS726040ALN610    | 4 TB   | 2       | 1239  | 0     | 3.40   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 2       | 1238  | 0     | 3.39   |
| WDC       | WD1600AAJS-00V4A0  | 160 GB | 1       | 1238  | 0     | 3.39   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 58      | 1457  | 1     | 3.36   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 1       | 3656  | 2     | 3.34   |
| Seagate   | ST3250312AS        | 250 GB | 5       | 1214  | 0     | 3.33   |
| WDC       | WD3201ABYS-01B9A0  | 320 GB | 1       | 1214  | 0     | 3.33   |
| Toshiba   | HDWA130            | 3 TB   | 1       | 1207  | 0     | 3.31   |
| WDC       | WD1600BEVT-22A23T0 | 160 GB | 2       | 1205  | 0     | 3.30   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 1       | 3610  | 2     | 3.30   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 3       | 1200  | 0     | 3.29   |
| HP        | FB160C4081         | 160 GB | 3       | 3161  | 3     | 3.27   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 3       | 1629  | 24    | 3.25   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 4       | 1181  | 0     | 3.24   |
| WDC       | WD3750LMCW-11D9GS3 | 375 GB | 1       | 1179  | 0     | 3.23   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 4       | 1171  | 0     | 3.21   |
| Samsung   | HD753LJ            | 752 GB | 3       | 1770  | 48    | 3.19   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 6       | 1273  | 1     | 3.19   |
| WDC       | WD1001FALS-403AA0  | 1 TB   | 3       | 1495  | 264   | 3.19   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 1       | 1158  | 0     | 3.17   |
| Samsung   | SP2504C            | 250 GB | 1       | 1158  | 0     | 3.17   |
| Seagate   | ST380815AS         | 80 GB  | 8       | 1442  | 550   | 3.17   |
| WDC       | WD10EURX-73C57Y0   | 1 TB   | 1       | 1156  | 0     | 3.17   |
| WDC       | WD800JD-08LSA0     | 80 GB  | 1       | 1155  | 0     | 3.17   |
| WDC       | WD20SMZW-11YFCS0   | 2 TB   | 1       | 1154  | 0     | 3.16   |
| HGST      | HDN728080ALE604    | 8 TB   | 7       | 1152  | 0     | 3.16   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 1       | 1146  | 0     | 3.14   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 10      | 1146  | 0     | 3.14   |
| WDC       | WD3000BLFS-60YBU2  | 304 GB | 2       | 1399  | 1     | 3.13   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 6       | 2271  | 46    | 3.13   |
| WDC       | WD7500BPVX-60JC3T0 | 752 GB | 1       | 1138  | 0     | 3.12   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 2       | 1133  | 0     | 3.10   |
| Seagate   | ST3320613AS        | 320 GB | 2       | 1995  | 11    | 3.10   |
| Hitachi   | HDS5C1050CLA382    | 500 GB | 1       | 1122  | 0     | 3.08   |
| WDC       | WD3200JS-22PDB0    | 320 GB | 1       | 1122  | 0     | 3.08   |
| Seagate   | ST500DM009-2DM14C  | 500 GB | 1       | 1122  | 0     | 3.08   |
| WDC       | WD2005FBYZ-01YCBB1 | 2 TB   | 2       | 1111  | 0     | 3.05   |
| WDC       | WD360GD-00FLC0     | 37 GB  | 1       | 1099  | 0     | 3.01   |
| WDC       | WD5000BEKT-22KA9T0 | 500 GB | 1       | 1085  | 0     | 2.97   |
| Samsung   | HD250HJ            | 250 GB | 1       | 1084  | 0     | 2.97   |
| Seagate   | ST320VT000-1BS14C  | 320 GB | 1       | 1083  | 0     | 2.97   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 3       | 1073  | 0     | 2.94   |
| WDC       | WD10EADX-00TDHB0   | 1 TB   | 1       | 1070  | 0     | 2.93   |
| Toshiba   | MQ01UBB200         | 2 TB   | 1       | 1067  | 0     | 2.93   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 13      | 1142  | 1     | 2.91   |
| HGST      | HUS724040ALA640    | 4 TB   | 5       | 1058  | 0     | 2.90   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 1       | 1057  | 0     | 2.90   |
| Seagate   | ST3160023A         | 160 GB | 1       | 1056  | 0     | 2.89   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 1       | 1053  | 0     | 2.89   |
| WDC       | WD1200BEVS-07RST0  | 120 GB | 1       | 1052  | 0     | 2.88   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 3       | 1273  | 1     | 2.88   |
| Toshiba   | DT01ACA300         | 3 TB   | 12      | 1253  | 86    | 2.87   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 5       | 1657  | 2     | 2.85   |
| Toshiba   | MQ01ABD100H        | 1 TB   | 2       | 1041  | 0     | 2.85   |
| HGST      | HDN726040ALE614    | 4 TB   | 4       | 1032  | 0     | 2.83   |
| WDC       | WD2000JB-00FUA0    | 200 GB | 1       | 1023  | 0     | 2.81   |
| Toshiba   | MC04ACA400E        | 4 TB   | 2       | 1023  | 0     | 2.80   |
| WDC       | WD1600AAJS-40H3A0  | 160 GB | 1       | 1022  | 0     | 2.80   |
| Seagate   | ST32000542AS       | 2 TB   | 2       | 1508  | 482   | 2.80   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 6       | 1317  | 169   | 2.79   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 2       | 1018  | 0     | 2.79   |
| Samsung   | HD103UJ            | 1 TB   | 9       | 1787  | 27    | 2.79   |
| ExcelStor | J8160              | 164 GB | 2       | 1015  | 0     | 2.78   |
| WDC       | WD2500AAKX-073CA1  | 250 GB | 1       | 1007  | 0     | 2.76   |
| Samsung   | HD251HJ            | 250 GB | 1       | 1006  | 0     | 2.76   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 1       | 1005  | 0     | 2.76   |
| HPE       | MB4000GVYZK        | 4 TB   | 8       | 1005  | 0     | 2.76   |
| Seagate   | ST33000651AS       | 3 TB   | 2       | 1003  | 0     | 2.75   |
| Toshiba   | HDWE150            | 5 TB   | 6       | 1186  | 5     | 2.73   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 8       | 1208  | 252   | 2.73   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 1       | 991   | 0     | 2.72   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 2       | 990   | 0     | 2.71   |
| Samsung   | HM500JI            | 500 GB | 4       | 1248  | 53    | 2.71   |
| Seagate   | ST9160411AS        | 160 GB | 2       | 1221  | 3     | 2.68   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 18      | 1100  | 65    | 2.67   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 4       | 1833  | 326   | 2.67   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 4       | 968   | 0     | 2.65   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 1449  | 1     | 2.65   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 2       | 965   | 0     | 2.65   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 3       | 965   | 0     | 2.65   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 18      | 1150  | 57    | 2.63   |
| Samsung   | HD203WI            | 2 TB   | 1       | 959   | 0     | 2.63   |
| Hitachi   | HTS727550A9E364    | 500 GB | 4       | 1013  | 32    | 2.62   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 5       | 1613  | 3     | 2.62   |
| WDC       | WD5000BEVT-22ZAT0  | 500 GB | 1       | 954   | 0     | 2.61   |
| Toshiba   | MQ01ABB200         | 2 TB   | 1       | 953   | 0     | 2.61   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 4       | 950   | 0     | 2.60   |
| Seagate   | ST3000DM003-2AE16L | 3 TB   | 1       | 947   | 0     | 2.60   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 4       | 1105  | 2     | 2.59   |
| Seagate   | ST3750528AS        | 752 GB | 3       | 1686  | 45    | 2.57   |
| WDC       | WD3200BEVS-08VAT2  | 320 GB | 1       | 936   | 0     | 2.57   |
| Seagate   | ST31000524AS       | 1 TB   | 7       | 1100  | 3     | 2.56   |
| CLOVER    | CD253GJ            | 250 GB | 1       | 928   | 0     | 2.54   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 6       | 1151  | 110   | 2.54   |
| Seagate   | ST1000NM0011       | 1 TB   | 3       | 1743  | 11    | 2.52   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 3       | 1053  | 3     | 2.52   |
| Samsung   | HD321HJ            | 320 GB | 1       | 914   | 0     | 2.51   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 2       | 1999  | 3     | 2.50   |
| Seagate   | ST3500312CS        | 500 GB | 12      | 1060  | 80    | 2.49   |
| WDC       | WD7500BPKT-22PK4T0 | 752 GB | 1       | 910   | 0     | 2.49   |
| Toshiba   | MQ04UBD200         | 2 TB   | 1       | 906   | 0     | 2.48   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 6       | 1575  | 3     | 2.48   |
| HGST      | HDN721010ALE604    | 10 TB  | 3       | 904   | 0     | 2.48   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1316  | 6     | 2.47   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 16      | 934   | 2     | 2.46   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 2       | 1719  | 1     | 2.45   |
| Seagate   | ST3160318AS        | 160 GB | 8       | 1259  | 67    | 2.44   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 3       | 1105  | 400   | 2.42   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 1       | 882   | 0     | 2.42   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 7       | 879   | 0     | 2.41   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 3       | 2362  | 79    | 2.39   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 7       | 1176  | 3     | 2.39   |
| WDC       | WD1600AAJS-60B4A0  | 160 GB | 1       | 872   | 0     | 2.39   |
| HGST      | HTE725032A7E630    | 320 GB | 3       | 1034  | 2     | 2.39   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 11      | 1073  | 38    | 2.38   |
| Samsung   | HD154UI            | 1.5 TB | 4       | 1849  | 38    | 2.38   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 5       | 1059  | 2     | 2.37   |
| Seagate   | ST320410A          | 20 GB  | 1       | 2579  | 2     | 2.36   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 1       | 856   | 0     | 2.35   |
| Maxtor    | STM3250310AS       | 250 GB | 4       | 927   | 1     | 2.34   |
| Hitachi   | HTS543216L9SA02    | 160 GB | 1       | 851   | 0     | 2.33   |
| WDC       | WD2500BEVT-00A23T0 | 250 GB | 1       | 851   | 0     | 2.33   |
| WDC       | WD80PURZ-85YNPY0   | 8 TB   | 1       | 851   | 0     | 2.33   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 2       | 1241  | 3     | 2.33   |
| Seagate   | ST91000640NS       | 1 TB   | 2       | 847   | 0     | 2.32   |
| Toshiba   | MD04ACA400         | 4 TB   | 3       | 893   | 3     | 2.32   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 1       | 842   | 0     | 2.31   |
| Seagate   | ST14000NM0018-2... | 14 TB  | 2       | 840   | 0     | 2.30   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 2       | 836   | 0     | 2.29   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 4       | 1142  | 2     | 2.29   |
| Toshiba   | MK1032GAX          | 100 GB | 1       | 830   | 0     | 2.27   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 6       | 828   | 0     | 2.27   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 3       | 1049  | 3     | 2.25   |
| WDC       | WD1200BB-00HTA0    | 120 GB | 2       | 1633  | 347   | 2.24   |
| Toshiba   | MG03ACA100         | 1 TB   | 9       | 817   | 0     | 2.24   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 1       | 816   | 0     | 2.24   |
| Seagate   | ST3500413AS        | 500 GB | 15      | 1216  | 334   | 2.23   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 2       | 810   | 0     | 2.22   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 2       | 810   | 0     | 2.22   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 5       | 1292  | 4     | 2.21   |
| Hitachi   | HDS721050CLA660    | 500 GB | 3       | 1969  | 676   | 2.21   |
| WDC       | WD2500JS-58NCB1    | 250 GB | 1       | 805   | 0     | 2.21   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 3       | 1323  | 33    | 2.21   |
| Toshiba   | MK4032GAX          | 40 GB  | 1       | 802   | 0     | 2.20   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 2       | 802   | 0     | 2.20   |
| Lenovo    | WD2004FBYZ-23YC... | 2 TB   | 4       | 802   | 0     | 2.20   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 1       | 799   | 0     | 2.19   |
| WDC       | WD10JQLX-22JFGT0   | 1 TB   | 1       | 790   | 0     | 2.17   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 1       | 790   | 0     | 2.17   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 4       | 789   | 0     | 2.16   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 29      | 1004  | 48    | 2.15   |
| WDC       | WD3000JS-63PDB1    | 304 GB | 1       | 783   | 0     | 2.15   |
| HP        | VB0250EAVER        | 250 GB | 1       | 2348  | 2     | 2.14   |
| WDC       | WD2500BEKT-75PVMT0 | 250 GB | 1       | 782   | 0     | 2.14   |
| WDC       | WD5000BPKT-60PK4T0 | 500 GB | 1       | 781   | 0     | 2.14   |
| HGST      | HUH728080ALE600    | 8 TB   | 1       | 777   | 0     | 2.13   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 8       | 886   | 1     | 2.12   |
| WDC       | WD15EARS-00Z5B1    | 1.5 TB | 1       | 3841  | 4     | 2.11   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 8       | 1776  | 546   | 2.10   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 9       | 764   | 0     | 2.09   |
| HGST      | HUS726040ALE610    | 4 TB   | 2       | 763   | 0     | 2.09   |
| Seagate   | ST380817AS         | 80 GB  | 4       | 760   | 0     | 2.08   |
| Seagate   | ST380013AS         | 80 GB  | 4       | 1678  | 3     | 2.08   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 2       | 754   | 0     | 2.07   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 2       | 753   | 0     | 2.06   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 1       | 751   | 0     | 2.06   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 4       | 790   | 93    | 2.05   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 7       | 736   | 0     | 2.02   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 1       | 734   | 0     | 2.01   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 12      | 1050  | 155   | 2.00   |
| Seagate   | ST3000VN007-2AH16M | 3 TB   | 1       | 729   | 0     | 2.00   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 8       | 728   | 0     | 2.00   |
| WDC       | WD1002FBYS-50A6B1  | 1 TB   | 1       | 727   | 0     | 1.99   |
| Samsung   | HD080HJ-P          | 80 GB  | 1       | 727   | 0     | 1.99   |
| Seagate   | ST31000424CS       | 1 TB   | 1       | 721   | 0     | 1.98   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 12      | 1301  | 186   | 1.96   |
| WDC       | WD5000LPVT-75G33T0 | 500 GB | 1       | 708   | 0     | 1.94   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 1       | 707   | 0     | 1.94   |
| Maxtor    | 6V160E0            | 160 GB | 1       | 704   | 0     | 1.93   |
| Seagate   | ST500DM002-1SB10A  | 500 GB | 2       | 703   | 0     | 1.93   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 4       | 1849  | 4     | 1.92   |
| HGST      | HUS722T2TALA600    | 2 TB   | 1       | 700   | 0     | 1.92   |
| WDC       | WD800BEVS-00RST0   | 80 GB  | 1       | 700   | 0     | 1.92   |
| Hitachi   | H7210CA30SUN1.0T   | 1 TB   | 1       | 696   | 0     | 1.91   |
| Samsung   | HD103SI            | 1 TB   | 5       | 823   | 606   | 1.91   |
| Toshiba   | MK2561GSY          | 250 GB | 1       | 695   | 0     | 1.91   |
| Seagate   | ST2000NM0011       | 2 TB   | 1       | 2080  | 2     | 1.90   |
| Toshiba   | MK1002TSKB         | 1 TB   | 1       | 692   | 0     | 1.90   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 11      | 692   | 0     | 1.90   |
| Seagate   | ST3320620NS        | 320 GB | 1       | 2076  | 2     | 1.90   |
| Samsung   | HM250HI            | 250 GB | 5       | 690   | 0     | 1.89   |
| Hitachi   | HDP725025GLA380    | 250 GB | 2       | 938   | 2     | 1.89   |
| WDC       | WD10JPVX-00JC3T0   | 1 TB   | 4       | 688   | 0     | 1.89   |
| WDC       | WD1600BEVT-75ZCT2  | 160 GB | 3       | 686   | 0     | 1.88   |
| Seagate   | ST2000NM0018-2F... | 2 TB   | 1       | 684   | 0     | 1.88   |
| WDC       | WD10JPVX-35JC3T0   | 1 TB   | 1       | 682   | 0     | 1.87   |
| MaxDig... | MD4000GSA6472E     | 4 TB   | 1       | 681   | 0     | 1.87   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 1       | 678   | 0     | 1.86   |
| Toshiba   | DT01ACA100         | 1 TB   | 31      | 697   | 1     | 1.84   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 3       | 666   | 0     | 1.83   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 5       | 665   | 0     | 1.82   |
| Seagate   | ST3250318AS        | 250 GB | 7       | 1117  | 128   | 1.82   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 3       | 885   | 1     | 1.77   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 11      | 647   | 0     | 1.77   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 3       | 1064  | 3     | 1.77   |
| Hitachi   | HTS723225L9A360    | 250 GB | 1       | 644   | 0     | 1.77   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 4       | 644   | 0     | 1.77   |
| WDC       | WD7500BPKX-75HPJT0 | 752 GB | 1       | 642   | 0     | 1.76   |
| Fujitsu   | MHW2120BH          | 120 GB | 1       | 641   | 0     | 1.76   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 5       | 648   | 5     | 1.75   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 5       | 635   | 0     | 1.74   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 4       | 629   | 0     | 1.73   |
| Seagate   | ST500NM0011        | 500 GB | 3       | 2025  | 13    | 1.72   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 1       | 625   | 0     | 1.71   |
| Hitachi   | HTS545025B9A300    | 250 GB | 5       | 676   | 403   | 1.71   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 2       | 623   | 0     | 1.71   |
| Seagate   | ST3160811AS        | 160 GB | 1       | 620   | 0     | 1.70   |
| Apple     | HDD ST1000LM024    | 1 TB   | 1       | 617   | 0     | 1.69   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 75      | 622   | 1     | 1.69   |
| Seagate   | ST3000DM003-1F216N | 3 TB   | 1       | 617   | 0     | 1.69   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 615   | 0     | 1.69   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 1       | 614   | 0     | 1.68   |
| WDC       | WD2500AAKX-19U6AA0 | 250 GB | 1       | 613   | 0     | 1.68   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 5       | 613   | 0     | 1.68   |
| WDC       | WD1600JS-00NCB1    | 160 GB | 1       | 611   | 0     | 1.68   |
| WDC       | WD3001FFSX-68JNUN0 | 3 TB   | 1       | 611   | 0     | 1.67   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 16      | 635   | 1     | 1.67   |
| WDC       | WD2500LPCX-24C6HT0 | 250 GB | 1       | 608   | 0     | 1.67   |
| HPE       | MB0500GCEHE        | 500 GB | 6       | 645   | 2     | 1.66   |
| Samsung   | HD161HJ            | 160 GB | 4       | 607   | 0     | 1.66   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 6       | 606   | 0     | 1.66   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 2       | 605   | 0     | 1.66   |
| WDC       | WD2500AAJS-40RYA0  | 250 GB | 1       | 603   | 0     | 1.65   |
| WDC       | WD2500JS-40TGB0    | 250 GB | 1       | 602   | 0     | 1.65   |
| Toshiba   | DT01ACA050         | 500 GB | 16      | 707   | 12    | 1.65   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 4       | 793   | 416   | 1.63   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 1       | 596   | 0     | 1.63   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 1       | 596   | 0     | 1.63   |
| Toshiba   | MQ04UBF100         | 1 TB   | 1       | 592   | 0     | 1.62   |
| WDC       | WD2000JB-00GVC0    | 200 GB | 1       | 3539  | 5     | 1.62   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 3       | 588   | 0     | 1.61   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 5       | 815   | 2     | 1.61   |
| Seagate   | ST3160813AS        | 160 GB | 3       | 868   | 2     | 1.61   |
| WDC       | WD3200BEKT-60PVMT0 | 320 GB | 2       | 582   | 0     | 1.60   |
| WDC       | WD4000AAKS-00TMA0  | 400 GB | 1       | 579   | 0     | 1.59   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 7       | 988   | 4     | 1.59   |
| Hitachi   | HDP725050GLA360    | 500 GB | 2       | 1148  | 19    | 1.58   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 2       | 575   | 0     | 1.58   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 3       | 573   | 0     | 1.57   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 4       | 571   | 0     | 1.57   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 3       | 1376  | 3     | 1.57   |
| Samsung   | HM500JJ            | 500 GB | 1       | 571   | 0     | 1.57   |
| Toshiba   | MQ01ACF050         | 500 GB | 6       | 569   | 0     | 1.56   |
| WDC       | WD5000BEKT-60KA9T0 | 500 GB | 1       | 569   | 0     | 1.56   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 5       | 753   | 4     | 1.56   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 7       | 562   | 0     | 1.54   |
| Hitachi   | HDS721050CLA362    | 500 GB | 4       | 615   | 254   | 1.53   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 4       | 556   | 0     | 1.53   |
| Seagate   | ST3320620AS        | 320 GB | 5       | 1278  | 197   | 1.52   |
| Fujitsu   | MHV2100BH PL       | 100 GB | 1       | 553   | 0     | 1.52   |
| WDC       | WD800BEVT-75ZCT2   | 80 GB  | 1       | 551   | 0     | 1.51   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 2       | 551   | 0     | 1.51   |
| Samsung   | HD160JJ-P          | 160 GB | 1       | 547   | 0     | 1.50   |
| Seagate   | ST3500418AS        | 500 GB | 19      | 1360  | 58    | 1.49   |
| WDC       | WD5000BPVT-16HXZT3 | 500 GB | 1       | 541   | 0     | 1.48   |
| Toshiba   | HDWN180            | 8 TB   | 10      | 540   | 0     | 1.48   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 9       | 539   | 0     | 1.48   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 2       | 587   | 11    | 1.48   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 2       | 537   | 0     | 1.47   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 2       | 1990  | 22    | 1.47   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 47      | 915   | 239   | 1.47   |
| Hitachi   | HTS725050A7E630    | 500 GB | 1       | 535   | 0     | 1.47   |
| WDC       | WD3200AAKS-00V6A0  | 320 GB | 1       | 533   | 0     | 1.46   |
| WDC       | WD3000F9YZ-09N20L1 | 3 TB   | 1       | 530   | 0     | 1.45   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 10      | 553   | 1     | 1.45   |
| IBM       | DBCA-204860        | 4 GB   | 1       | 522   | 0     | 1.43   |
| Seagate   | ST9160310AS        | 160 GB | 1       | 2600  | 4     | 1.43   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 7       | 519   | 0     | 1.42   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 1       | 517   | 0     | 1.42   |
| WDC       | WD5000AAKX-08ANVA0 | 500 GB | 1       | 516   | 0     | 1.42   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 1       | 516   | 0     | 1.41   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 4       | 516   | 0     | 1.41   |
| WDC       | WD10SPZX-75Z10T1   | 1 TB   | 1       | 516   | 0     | 1.41   |
| Seagate   | ST3320820AS        | 320 GB | 2       | 510   | 0     | 1.40   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 2       | 936   | 4     | 1.39   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 6       | 798   | 89    | 1.39   |
| WDC       | WD400BD-75LRA0     | 40 GB  | 1       | 503   | 0     | 1.38   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 1       | 502   | 0     | 1.38   |
| Seagate   | ST3750640AS        | 752 GB | 2       | 1505  | 2     | 1.38   |
| Hitachi   | HDS721616PLA380    | 160 GB | 1       | 500   | 0     | 1.37   |
| WDC       | WD800AAJS-60WAA0   | 80 GB  | 1       | 1472  | 2     | 1.34   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 6       | 490   | 0     | 1.34   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 2       | 486   | 0     | 1.33   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 15      | 543   | 1     | 1.33   |
| Maxtor    | 6E040T0            | 40 GB  | 1       | 482   | 0     | 1.32   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 1       | 479   | 0     | 1.31   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 28      | 545   | 7     | 1.31   |
| HGST      | HTS721010A9E630    | 1 TB   | 21      | 529   | 147   | 1.31   |
| Toshiba   | MQ01UBD100         | 1 TB   | 1       | 944   | 1     | 1.29   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 6       | 470   | 0     | 1.29   |
| Samsung   | HD322HJ            | 320 GB | 7       | 733   | 86    | 1.28   |
| HGST      | HTS541010A9E680    | 1 TB   | 14      | 544   | 295   | 1.28   |
| Seagate   | ST6000NE0023-2E... | 6 TB   | 2       | 840   | 4     | 1.28   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 7       | 464   | 0     | 1.27   |
| Seagate   | ST3320418AS        | 320 GB | 6       | 926   | 357   | 1.27   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 27      | 583   | 2     | 1.26   |
| Toshiba   | MK1655GSX          | 160 GB | 1       | 459   | 0     | 1.26   |
| WDC       | WD10PURX-64E5EY0   | 1 TB   | 1       | 917   | 1     | 1.26   |
| Fujitsu   | MHY2120BH          | 120 GB | 2       | 456   | 0     | 1.25   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 1       | 455   | 0     | 1.25   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 11      | 455   | 0     | 1.25   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 4       | 507   | 2     | 1.24   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 1       | 446   | 0     | 1.22   |
| Seagate   | ST9120821AS        | 120 GB | 1       | 445   | 0     | 1.22   |
| Hitachi   | HDT725032VLA380    | 320 GB | 2       | 441   | 0     | 1.21   |
| Seagate   | ST9250315AS        | 250 GB | 4       | 609   | 253   | 1.21   |
| WDC       | WD2000JS-55MHB0    | 192 GB | 1       | 439   | 0     | 1.20   |
| Seagate   | ST9160412ASG       | 160 GB | 1       | 436   | 0     | 1.20   |
| WDC       | WD7500BPKX-22HPJT0 | 752 GB | 1       | 434   | 0     | 1.19   |
| WDC       | WD2500YS-01SHB1    | 256 GB | 1       | 433   | 0     | 1.19   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 2       | 694   | 1     | 1.18   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 1       | 429   | 0     | 1.18   |
| WDC       | WD10SPCX-24HWST1   | 1 TB   | 1       | 429   | 0     | 1.18   |
| Fujitsu   | MHT2080AH          | 80 GB  | 1       | 427   | 0     | 1.17   |
| WDC       | WD2000FYYZ         | 2 TB   | 2       | 1353  | 3     | 1.17   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 1       | 424   | 0     | 1.16   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 1       | 422   | 0     | 1.16   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 6       | 1457  | 256   | 1.14   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 3       | 415   | 0     | 1.14   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 8       | 414   | 0     | 1.13   |
| WDC       | WD3200BPVT-22ZEST0 | 320 GB | 1       | 410   | 0     | 1.12   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 4       | 406   | 0     | 1.11   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 2       | 406   | 0     | 1.11   |
| Seagate   | ST2000DX001-1CM164 | 2 TB   | 1       | 406   | 0     | 1.11   |
| Seagate   | ST9250410ASG       | 250 GB | 2       | 404   | 0     | 1.11   |
| HGST      | HUS722T2TALA604    | 2 TB   | 4       | 544   | 4     | 1.11   |
| Hitachi   | HTS723220L9A360    | 200 GB | 1       | 401   | 0     | 1.10   |
| WDC       | WD2500BEVS-22UST0  | 250 GB | 2       | 397   | 0     | 1.09   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 2       | 396   | 0     | 1.09   |
| Toshiba   | HDWD130            | 3 TB   | 12      | 413   | 1     | 1.07   |
| WDC       | WD1600BEVT-11ZCT0  | 160 GB | 1       | 392   | 0     | 1.07   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 1       | 1545  | 3     | 1.06   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 3       | 385   | 0     | 1.06   |
| Seagate   | ST3250310AS        | 250 GB | 4       | 1321  | 514   | 1.05   |
| Seagate   | ST31500541AS       | 1.5 TB | 7       | 998   | 173   | 1.05   |
| Seagate   | ST380811AS         | 80 GB  | 1       | 383   | 0     | 1.05   |
| Toshiba   | MG04ACA600E        | 6 TB   | 2       | 382   | 0     | 1.05   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 1       | 382   | 0     | 1.05   |
| HGST      | HUS726020ALA610    | 2 TB   | 1       | 381   | 0     | 1.04   |
| WDC       | WD5000HHTZ-75N21V0 | 500 GB | 1       | 380   | 0     | 1.04   |
| Apple     | HDD HTS541010A9... | 1 TB   | 3       | 649   | 2     | 1.04   |
| Toshiba   | MK1517GAP          | 16 GB  | 1       | 380   | 0     | 1.04   |
| HGST      | HUS726020ALE610    | 2 TB   | 2       | 380   | 0     | 1.04   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 9       | 460   | 2     | 1.04   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 8       | 377   | 0     | 1.04   |
| WDC       | WD10EZEX-08Y20A0   | 1 TB   | 1       | 377   | 0     | 1.03   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 2       | 377   | 0     | 1.03   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 2       | 376   | 0     | 1.03   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 2       | 375   | 0     | 1.03   |
| WDC       | WD40NMZW-59GX6S1   | 4 TB   | 2       | 373   | 0     | 1.02   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 3       | 371   | 0     | 1.02   |
| Seagate   | ST9160821A         | 160 GB | 1       | 371   | 0     | 1.02   |
| HPE       | MB4000GCWLV        | 4 TB   | 4       | 366   | 0     | 1.00   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 8       | 366   | 0     | 1.00   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 3       | 544   | 196   | 1.00   |
| Seagate   | ST3160815AS        | 160 GB | 8       | 1393  | 136   | 1.00   |
| Toshiba   | HDWD120            | 2 TB   | 7       | 367   | 3     | 0.99   |
| Seagate   | ST3250620AS        | 250 GB | 1       | 1081  | 2     | 0.99   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 1       | 357   | 0     | 0.98   |
| Fujitsu   | MHZ2120BH G2       | 120 GB | 1       | 357   | 0     | 0.98   |
| Seagate   | ST500LX025-1U717D  | 500 GB | 2       | 355   | 0     | 0.97   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 9       | 353   | 0     | 0.97   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 3       | 466   | 3     | 0.96   |
| Seagate   | ST3120827AS        | 120 GB | 1       | 348   | 0     | 0.95   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 15      | 347   | 0     | 0.95   |
| HGST      | HTS725032A7E630    | 320 GB | 7       | 731   | 21    | 0.95   |
| Toshiba   | MN07ACA12T         | 12 TB  | 2       | 345   | 0     | 0.95   |
| Seagate   | ST3160812AS        | 160 GB | 3       | 845   | 435   | 0.94   |
| WDC       | WD10EARS-003BB1    | 1 TB   | 1       | 1712  | 4     | 0.94   |
| HGST      | HTS545050A7E680    | 500 GB | 10      | 402   | 103   | 0.94   |
| WDC       | WD5000LPVT-80G33T2 | 500 GB | 1       | 341   | 0     | 0.93   |
| WDC       | WD5000BPVT-22HXZT3 | 500 GB | 2       | 881   | 510   | 0.93   |
| Seagate   | ST980313AS         | 80 GB  | 1       | 338   | 0     | 0.93   |
| Seagate   | ST2000NE0025-2F... | 2 TB   | 2       | 338   | 0     | 0.93   |
| Seagate   | ST3250824AS Q      | 250 GB | 1       | 338   | 0     | 0.93   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 3       | 673   | 346   | 0.92   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 1       | 1677  | 4     | 0.92   |
| Toshiba   | MK2546GSX          | 250 GB | 2       | 604   | 17    | 0.92   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 26      | 333   | 0     | 0.91   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 3       | 332   | 0     | 0.91   |
| Samsung   | HM320II            | 320 GB | 2       | 331   | 0     | 0.91   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 2       | 330   | 0     | 0.91   |
| Toshiba   | HDWE160            | 6 TB   | 4       | 330   | 0     | 0.91   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 1       | 328   | 0     | 0.90   |
| Seagate   | ST9250315ASG       | 250 GB | 1       | 327   | 0     | 0.90   |
| Toshiba   | MK3259GSXP         | 320 GB | 1       | 326   | 0     | 0.89   |
| WDC       | WD20PURX-89P6ZY0   | 2 TB   | 1       | 1630  | 4     | 0.89   |
| WDC       | WD3200AVVS-63L2B0  | 320 GB | 1       | 324   | 0     | 0.89   |
| MediaMax  | WL2000GSA6454      | 2 TB   | 3       | 697   | 6     | 0.89   |
| HGST      | HTS545032A7E680    | 320 GB | 1       | 321   | 0     | 0.88   |
| Toshiba   | DT01ABA300         | 3 TB   | 3       | 622   | 3     | 0.88   |
| WDC       | WD5000AAVS-00G9B1  | 500 GB | 1       | 1921  | 5     | 0.88   |
| WDC       | WD20NMVW-59EDZS7   | 2 TB   | 1       | 320   | 0     | 0.88   |
| Toshiba   | MK1637GSX          | 160 GB | 2       | 813   | 1     | 0.87   |
| Hitachi   | HTS723232A7A364    | 320 GB | 7       | 938   | 462   | 0.87   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 4       | 311   | 0     | 0.85   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 4       | 387   | 2     | 0.85   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 4       | 308   | 0     | 0.85   |
| WDC       | WD60EFRX-68TGBN1   | 6 TB   | 3       | 2362  | 7     | 0.84   |
| Seagate   | ST3120814A         | 120 GB | 1       | 3974  | 12    | 0.84   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 5       | 303   | 0     | 0.83   |
| Toshiba   | HDWG180            | 8 TB   | 1       | 303   | 0     | 0.83   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 15      | 302   | 0     | 0.83   |
| Fujitsu   | MJA2250BH FFS G1   | 250 GB | 1       | 302   | 0     | 0.83   |
| WDC       | WD7500AAVS-00D7B0  | 752 GB | 1       | 300   | 0     | 0.82   |
| Toshiba   | DT01ACA050 LENOVO  | 500 GB | 1       | 298   | 0     | 0.82   |
| Toshiba   | HDWQ140            | 4 TB   | 9       | 298   | 0     | 0.82   |
| Seagate   | ST3250823AS        | 250 GB | 1       | 2661  | 8     | 0.81   |
| Toshiba   | MK2546GSX_200      | 200 GB | 1       | 291   | 0     | 0.80   |
| Toshiba   | MQ01ABF032         | 320 GB | 2       | 289   | 0     | 0.79   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 25      | 324   | 5     | 0.79   |
| WDC       | WD5000AZRX-00L4HB0 | 500 GB | 1       | 288   | 0     | 0.79   |
| WDC       | WD5000LPCX-24C6HT0 | 500 GB | 4       | 286   | 0     | 0.78   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 17      | 284   | 0     | 0.78   |
| Seagate   | ST96023AS          | 58 GB  | 1       | 1419  | 4     | 0.78   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 2       | 1571  | 6     | 0.77   |
| WDC       | WD5000AAKX-083CA0  | 500 GB | 1       | 2482  | 8     | 0.76   |
| Hitachi   | HTS547550A9E384    | 500 GB | 6       | 445   | 196   | 0.75   |
| Toshiba   | MK3265GSXN         | 320 GB | 2       | 594   | 6     | 0.75   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 3       | 270   | 0     | 0.74   |
| Seagate   | ST9250827AS        | 250 GB | 4       | 490   | 9     | 0.74   |
| Toshiba   | MQ03UBB200         | 2 TB   | 2       | 269   | 0     | 0.74   |
| WDC       | WD3200BPVT-75JJ5T0 | 320 GB | 1       | 1075  | 3     | 0.74   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 5       | 333   | 2     | 0.73   |
| Seagate   | ST1000LM014-1EJ164 | 1 TB   | 3       | 400   | 15    | 0.72   |
| Hitachi   | HTS541080G9SA00    | 80 GB  | 1       | 525   | 1     | 0.72   |
| Seagate   | ST9500325AS        | 500 GB | 16      | 520   | 140   | 0.72   |
| Seagate   | ST3750640NS        | 752 GB | 2       | 2066  | 1043  | 0.71   |
| WDC       | WD3200BPVT-24JJ5T0 | 320 GB | 2       | 256   | 0     | 0.70   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 7       | 290   | 109   | 0.70   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 1       | 255   | 0     | 0.70   |
| Seagate   | ST3120211AS        | 120 GB | 1       | 508   | 1     | 0.70   |
| Samsung   | HD403LJ            | 400 GB | 1       | 254   | 0     | 0.70   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 3       | 368   | 23    | 0.70   |
| WDC       | WD10JMVW-11AJGS1   | 1 TB   | 2       | 837   | 5     | 0.69   |
| Fujitsu   | MHY2250BH          | 250 GB | 1       | 253   | 0     | 0.69   |
| Samsung   | HN-M101MBB         | 1 TB   | 2       | 251   | 0     | 0.69   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 10      | 409   | 102   | 0.69   |
| WDC       | WD5000LPVT-24G33T1 | 500 GB | 1       | 249   | 0     | 0.68   |
| WDC       | WD5000LPCX-60VHAT0 | 500 GB | 2       | 401   | 441   | 0.68   |
| WDC       | WD1600BEVS-08VAT2  | 160 GB | 3       | 404   | 1     | 0.68   |
| Toshiba   | MK1060GSCX         | 100 GB | 1       | 247   | 0     | 0.68   |
| WDC       | WD40E31X-00HY4A0   | 4 TB   | 1       | 245   | 0     | 0.67   |
| WDC       | WD20SDZW-11JJ8S0   | 2 TB   | 1       | 244   | 0     | 0.67   |
| Toshiba   | MQ01ABD100         | 1 TB   | 29      | 328   | 115   | 0.67   |
| Seagate   | ST980811AS         | 80 GB  | 2       | 243   | 0     | 0.67   |
| Seagate   | ST380215A          | 80 GB  | 1       | 242   | 0     | 0.66   |
| Seagate   | ST31000340NS       | 1 TB   | 1       | 2906  | 11    | 0.66   |
| Fujitsu   | MHT2080BH          | 80 GB  | 1       | 241   | 0     | 0.66   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 7       | 333   | 377   | 0.66   |
| Hitachi   | HTS545016B9SA02    | 160 GB | 2       | 507   | 5     | 0.66   |
| Toshiba   | MQ01ABD032         | 320 GB | 4       | 487   | 320   | 0.66   |
| Seagate   | ST3250410AS        | 250 GB | 4       | 586   | 5     | 0.65   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 17      | 257   | 99    | 0.65   |
| WDC       | WD7500BPVT-80HXZT3 | 752 GB | 2       | 566   | 4     | 0.65   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 7       | 235   | 0     | 0.65   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 1       | 234   | 0     | 0.64   |
| Samsung   | SP0812C            | 80 GB  | 1       | 234   | 0     | 0.64   |
| WDC       | WD120EFBX-68B0EN0  | 12 TB  | 2       | 234   | 0     | 0.64   |
| Hitachi   | HTS547575A9E384    | 752 GB | 3       | 373   | 343   | 0.64   |
| Apple     | HDD ST2000DM001    | 2 TB   | 1       | 232   | 0     | 0.64   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 6       | 231   | 0     | 0.64   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 7       | 230   | 0     | 0.63   |
| Samsung   | SP2514N            | 250 GB | 1       | 2529  | 10    | 0.63   |
| HGST      | HTS541075A7E630    | 752 GB | 2       | 321   | 507   | 0.62   |
| Hitachi   | HTE723225A7A364    | 250 GB | 1       | 227   | 0     | 0.62   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 1       | 678   | 2     | 0.62   |
| Hitachi   | HTS543232L9A300    | 320 GB | 1       | 223   | 0     | 0.61   |
| WDC       | WD5000AAKS-22A7B0  | 500 GB | 1       | 2901  | 12    | 0.61   |
| WDC       | WD40NDZW-11MR8S1   | 4 TB   | 1       | 222   | 0     | 0.61   |
| Seagate   | ST1000LX015-1U7172 | 1 TB   | 3       | 279   | 1344  | 0.60   |
| Toshiba   | HDWD110            | 1 TB   | 11      | 218   | 0     | 0.60   |
| Apple     | HDD HTS547575A9... | 752 GB | 1       | 217   | 0     | 0.60   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 1       | 652   | 2     | 0.60   |
| Toshiba   | MQ01ABF050M        | 500 GB | 1       | 217   | 0     | 0.60   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 22      | 227   | 7     | 0.59   |
| Seagate   | ST500LM000-1EJ162  | 500 GB | 3       | 213   | 0     | 0.58   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 2       | 1503  | 19    | 0.58   |
| WDC       | WD10SPZX-22Z10T0   | 1 TB   | 3       | 208   | 0     | 0.57   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 17      | 536   | 601   | 0.57   |
| Fujitsu   | MHY2160BH          | 160 GB | 1       | 206   | 0     | 0.57   |
| WDC       | WD20EARX-00ZUDB0   | 2 TB   | 1       | 2266  | 10    | 0.56   |
| WDC       | WD1600BEVT-22ZCT0  | 160 GB | 10      | 253   | 3     | 0.56   |
| Seagate   | ST96812AS          | 64 GB  | 5       | 216   | 1     | 0.56   |
| HGST      | HTS725050A7E630    | 500 GB | 18      | 556   | 580   | 0.56   |
| Fujitsu   | MHZ2320BH FFS G1   | 320 GB | 1       | 203   | 0     | 0.56   |
| Toshiba   | MQ01ACF032         | 320 GB | 4       | 341   | 248   | 0.56   |
| Hitachi   | HTS545032B9A302    | 320 GB | 1       | 605   | 2     | 0.55   |
| Toshiba   | MQ04UBB400         | 4 TB   | 1       | 201   | 0     | 0.55   |
| WDC       | WD3200AAJS-00L7A0  | 320 GB | 1       | 1806  | 8     | 0.55   |
| Samsung   | HD503HI            | 500 GB | 1       | 200   | 0     | 0.55   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 3       | 199   | 0     | 0.55   |
| WDC       | WD3200AAVS-00ZTB0  | 320 GB | 1       | 589   | 2     | 0.54   |
| Seagate   | ST9500420AS        | 500 GB | 10      | 695   | 948   | 0.54   |
| Seagate   | ST9320421ASG       | 320 GB | 1       | 195   | 0     | 0.54   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 1       | 195   | 0     | 0.54   |
| Toshiba   | MK1234GSX          | 120 GB | 2       | 194   | 0     | 0.53   |
| WDC       | WD5000AAKX-00U6AA0 | 500 GB | 1       | 385   | 1     | 0.53   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 1       | 192   | 0     | 0.53   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 5       | 476   | 218   | 0.52   |
| Seagate   | ST3500830AS        | 500 GB | 2       | 189   | 0     | 0.52   |
| Toshiba   | MK3263GSX          | 320 GB | 1       | 1135  | 5     | 0.52   |
| WDC       | WD5000LPVX-75V0TT0 | 500 GB | 2       | 188   | 0     | 0.52   |
| WDC       | WD1600BEVT-00A23T0 | 160 GB | 2       | 187   | 0     | 0.51   |
| WDC       | WD5000LPLX-66ZNTT0 | 500 GB | 1       | 186   | 0     | 0.51   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 2       | 185   | 0     | 0.51   |
| Hitachi   | HDT721064SLA360    | 640 GB | 2       | 990   | 4     | 0.51   |
| ExcelStor | J8160S             | 160 GB | 2       | 1003  | 15    | 0.51   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 4       | 355   | 64    | 0.50   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 3       | 183   | 0     | 0.50   |
| Samsung   | HD256GJ            | 250 GB | 1       | 1274  | 6     | 0.50   |
| WDC       | WD1600JS-56MHB1    | 160 GB | 1       | 909   | 4     | 0.50   |
| WDC       | WD1600BEKT-00PVMT0 | 160 GB | 1       | 181   | 0     | 0.50   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 4       | 822   | 276   | 0.49   |
| WDC       | WD4000BEVT-00ZAT0  | 400 GB | 1       | 179   | 0     | 0.49   |
| WDC       | WD7500BPKX-80HPJT0 | 752 GB | 1       | 178   | 0     | 0.49   |
| WDC       | WD20SPZX-22CRAT0   | 2 TB   | 1       | 177   | 0     | 0.49   |
| WDC       | WD5000BHTZ-50JCPV0 | 500 GB | 1       | 177   | 0     | 0.49   |
| HGST      | HTS541010B7E610    | 1 TB   | 6       | 177   | 0     | 0.49   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 9       | 176   | 0     | 0.48   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 1       | 3354  | 18    | 0.48   |
| Hitachi   | HTS545050A7E380    | 500 GB | 5       | 262   | 73    | 0.48   |
| WDC       | WD1005FBYZ-01YCBB3 | 1 TB   | 3       | 175   | 0     | 0.48   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 4       | 320   | 2     | 0.47   |
| Seagate   | ST1000VM002-1SD102 | 1 TB   | 3       | 579   | 3     | 0.47   |
| Toshiba   | MK5065GSXF         | 500 GB | 2       | 168   | 0     | 0.46   |
| Seagate   | ST3500410AS        | 500 GB | 1       | 337   | 1     | 0.46   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 1       | 1510  | 8     | 0.46   |
| WDC       | WD5000LPLX-60ZNTT1 | 500 GB | 2       | 212   | 1     | 0.46   |
| Seagate   | ST3500320NS        | 500 GB | 1       | 1324  | 7     | 0.45   |
| Hitachi   | HTS722010K9SA00    | 100 GB | 1       | 327   | 1     | 0.45   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 2       | 161   | 0     | 0.44   |
| Fujitsu   | MJA2250BH G2       | 250 GB | 1       | 161   | 0     | 0.44   |
| Toshiba   | MK1255GSX H        | 120 GB | 1       | 160   | 0     | 0.44   |
| WDC       | WD800BB-00HEA0     | 80 GB  | 1       | 4322  | 26    | 0.44   |
| WDC       | WD1600AAJS-75M0A0  | 160 GB | 2       | 828   | 5     | 0.43   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 27      | 196   | 82    | 0.43   |
| WDC       | WD1003FBYX-88 LEN  | 1 TB   | 1       | 466   | 2     | 0.43   |
| Seagate   | ST9750423AS        | 752 GB | 2       | 152   | 0     | 0.42   |
| Toshiba   | MQ01ABD050         | 500 GB | 5       | 418   | 413   | 0.42   |
| WDC       | WD3200BPVT-75ZEST0 | 320 GB | 3       | 273   | 3     | 0.41   |
| WDC       | WD5000AVCS-632DY1  | 500 GB | 1       | 1354  | 8     | 0.41   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 1       | 148   | 0     | 0.41   |
| WDC       | WD10JPVX-80JC3T0   | 1 TB   | 1       | 148   | 0     | 0.41   |
| Hitachi   | HTS541680J9SA00    | 80 GB  | 5       | 608   | 10    | 0.41   |
| WDC       | WD3200AAKX-753CA1  | 320 GB | 1       | 147   | 0     | 0.40   |
| WDC       | WD5000BPVT-08HXZT3 | 500 GB | 1       | 146   | 0     | 0.40   |
| WDC       | WD50EFRX-68L0BN1   | 5 TB   | 1       | 1314  | 8     | 0.40   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 2       | 146   | 0     | 0.40   |
| WDC       | WD30EZRX-22D8PB0   | 3 TB   | 1       | 875   | 5     | 0.40   |
| Seagate   | ST3320311CS        | 320 GB | 1       | 720   | 4     | 0.39   |
| WDC       | WD10SPZX-60Z10T0   | 1 TB   | 2       | 205   | 1     | 0.39   |
| WDC       | WD800JB-00JJC0     | 80 GB  | 1       | 2710  | 18    | 0.39   |
| WDC       | WD60EMAZ-11LW3B0   | 6 TB   | 1       | 142   | 0     | 0.39   |
| Toshiba   | HDWE140            | 4 TB   | 4       | 184   | 5     | 0.39   |
| WDC       | WD20EURX-63T0FY0   | 2 TB   | 2       | 1291  | 6     | 0.38   |
| WDC       | WD5000LPCX-75VHAT0 | 500 GB | 2       | 209   | 4     | 0.37   |
| WDC       | WD2500AAKS-60L9A0  | 250 GB | 1       | 1350  | 9     | 0.37   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 3       | 134   | 0     | 0.37   |
| WDC       | WD120EDAZ-11F3RA0  | 12 TB  | 9       | 131   | 0     | 0.36   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 4       | 129   | 0     | 0.36   |
| WDC       | WD5000AAKS-22V1A0  | 500 GB | 1       | 1163  | 8     | 0.35   |
| Toshiba   | MQ01ABF050         | 500 GB | 17      | 203   | 120   | 0.35   |
| Hitachi   | HTS545032B9A300    | 320 GB | 5       | 259   | 482   | 0.34   |
| WDC       | WD3200BEVT-22ZCT0  | 320 GB | 3       | 211   | 5     | 0.33   |
| WDC       | WD10EURX-83UY4Y0   | 1 TB   | 1       | 121   | 0     | 0.33   |
| WDC       | WD4000AAKS-00C8A0  | 400 GB | 1       | 3152  | 25    | 0.33   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 8       | 134   | 1     | 0.33   |
| Apple     | HDD HTS545050A7... | 500 GB | 4       | 157   | 6     | 0.33   |
| WDC       | WD10SPZX-08Z10     | 1 TB   | 3       | 120   | 0     | 0.33   |
| Seagate   | ST3120026A         | 120 GB | 1       | 1076  | 8     | 0.33   |
| WDC       | WD10JPLX-00MBPT1   | 1 TB   | 1       | 114   | 0     | 0.31   |
| Seagate   | ST500LM000-SSHD... | 500 GB | 3       | 398   | 337   | 0.31   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 1       | 571   | 4     | 0.31   |
| Toshiba   | MK1665GSX          | 160 GB | 1       | 114   | 0     | 0.31   |
| Seagate   | ST9500530NS 42D... | 500 GB | 2       | 221   | 48    | 0.31   |
| Toshiba   | MK2555GSX          | 250 GB | 3       | 744   | 468   | 0.31   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 4       | 309   | 2     | 0.30   |
| WDC       | WD20SPZX-75UA7T0   | 2 TB   | 1       | 109   | 0     | 0.30   |
| Hitachi   | HTS721010G9AT00    | 100 GB | 1       | 109   | 0     | 0.30   |
| HGST      | HTS545050A7E660    | 500 GB | 1       | 763   | 6     | 0.30   |
| WDC       | WD10SDRW-34A0XS0   | 1 TB   | 1       | 106   | 0     | 0.29   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 6       | 105   | 0     | 0.29   |
| WDC       | WD10SPZX-22Z10T1   | 1 TB   | 3       | 105   | 0     | 0.29   |
| WDC       | WD10EZEX-00BBHA0   | 1 TB   | 2       | 103   | 0     | 0.28   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 1       | 103   | 0     | 0.28   |
| WDC       | WD5000LPVX-80V0TT0 | 500 GB | 1       | 103   | 0     | 0.28   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 9       | 160   | 1     | 0.28   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 1       | 1338  | 12    | 0.28   |
| HGST      | HUH721010ALE604    | 10 TB  | 2       | 102   | 0     | 0.28   |
| Seagate   | ST31000524NS       | 1 TB   | 1       | 101   | 0     | 0.28   |
| Toshiba   | MK7575GSX          | 752 GB | 1       | 604   | 5     | 0.28   |
| WDC       | WD3200BEKX-00B7WT0 | 320 GB | 1       | 702   | 6     | 0.28   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 7       | 99    | 0     | 0.27   |
| WDC       | WD3200BEVT-80A0RT0 | 320 GB | 1       | 787   | 7     | 0.27   |
| Samsung   | HN-M500MBB         | 500 GB | 1       | 97    | 0     | 0.27   |
| WDC       | WD6400AAKS-22A7B0  | 640 GB | 2       | 904   | 9     | 0.26   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 2       | 192   | 1     | 0.26   |
| WDC       | WD10EADS-00P8B0    | 1 TB   | 2       | 218   | 4     | 0.26   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 1       | 94    | 0     | 0.26   |
| Seagate   | ST980813AS         | 80 GB  | 1       | 93    | 0     | 0.26   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 1       | 279   | 2     | 0.25   |
| Hitachi   | HTS543225L9A300    | 250 GB | 2       | 525   | 5     | 0.25   |
| Seagate   | ST9320423AS        | 320 GB | 6       | 675   | 815   | 0.25   |
| WDC       | WD3200AAJS-22B4A0  | 320 GB | 2       | 1829  | 50    | 0.25   |
| Hitachi   | HTS542516K9SA00    | 160 GB | 1       | 453   | 4     | 0.25   |
| Seagate   | ST500LT035-1E9G42  | 500 GB | 1       | 89    | 0     | 0.24   |
| WDC       | WD1600AAJS-00WAA0  | 160 GB | 2       | 97    | 1     | 0.24   |
| Seagate   | STEC PATA          | 8 GB   | 1       | 87    | 0     | 0.24   |
| WDC       | WD10JMVW-11AJGS0   | 1 TB   | 2       | 267   | 6     | 0.24   |
| Hitachi   | HTS542580K9SA00    | 80 GB  | 1       | 85    | 0     | 0.23   |
| WDC       | WD5003ABYX-23 8... | 500 GB | 1       | 1183  | 13    | 0.23   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 9       | 390   | 231   | 0.23   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 2       | 701   | 4     | 0.23   |
| Toshiba   | MK8034GSX          | 80 GB  | 1       | 416   | 4     | 0.23   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 2       | 163   | 1     | 0.22   |
| WDC       | WD60EZRZ-22GZ5B1   | 6 TB   | 1       | 81    | 0     | 0.22   |
| HGST      | HUS722T1TALA600    | 1 TB   | 1       | 80    | 0     | 0.22   |
| Seagate   | ST4000NM002A-2H... | 4 TB   | 2       | 79    | 0     | 0.22   |
| WDC       | WUH721414ALE6L4    | 14 TB  | 1       | 79    | 0     | 0.22   |
| WDC       | WD20EZRZ-22Z5HB0   | 2 TB   | 1       | 79    | 0     | 0.22   |
| Seagate   | ST31000528AS       | 1 TB   | 8       | 774   | 168   | 0.22   |
| Toshiba   | MQ04ABF100         | 1 TB   | 12      | 98    | 1     | 0.21   |
| WDC       | WD5000BPVX-00JC3T0 | 500 GB | 1       | 76    | 0     | 0.21   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 1       | 650   | 8     | 0.20   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 1       | 72    | 0     | 0.20   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 5       | 71    | 0     | 0.20   |
| WDC       | WD3200BPVT-55ZEST0 | 320 GB | 1       | 142   | 1     | 0.20   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 2       | 71    | 0     | 0.20   |
| Toshiba   | MK6006GAH          | 64 GB  | 1       | 426   | 5     | 0.19   |
| Hitachi   | HCC545016B9A300    | 160 GB | 1       | 70    | 0     | 0.19   |
| WDC       | WD5000LPVX-00V0TT0 | 500 GB | 1       | 70    | 0     | 0.19   |
| Hitachi   | HTS543232A7A384    | 320 GB | 5       | 310   | 429   | 0.19   |
| Seagate   | ST980310AS         | 80 GB  | 1       | 345   | 4     | 0.19   |
| Toshiba   | MQ01ABD075         | 752 GB | 3       | 636   | 45    | 0.19   |
| Fujitsu   | MHZ2250BH G1       | 250 GB | 1       | 673   | 9     | 0.18   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 1       | 67    | 0     | 0.18   |
| Seagate   | ST9120822AS        | 120 GB | 2       | 562   | 6     | 0.18   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 8       | 1289  | 885   | 0.18   |
| WDC       | WD20SPZX-22UA7T0   | 2 TB   | 6       | 64    | 0     | 0.18   |
| WDC       | WD5000BEVT-24A0RT0 | 500 GB | 1       | 62    | 0     | 0.17   |
| Toshiba   | MQ02ABF050H        | 500 GB | 2       | 61    | 0     | 0.17   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 1       | 61    | 0     | 0.17   |
| Apple     | HDD HTS541010A9... | 1 TB   | 1       | 61    | 0     | 0.17   |
| Samsung   | HM160HI            | 160 GB | 6       | 329   | 46    | 0.17   |
| Toshiba   | MG09ACA18TE        | 18 TB  | 2       | 60    | 0     | 0.17   |
| WDC       | WD3200BEVT-00A0RT0 | 320 GB | 2       | 576   | 11    | 0.16   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 8       | 461   | 765   | 0.16   |
| Hitachi   | HTS722020K9SA00    | 200 GB | 1       | 234   | 3     | 0.16   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 1       | 343   | 5     | 0.16   |
| WDC       | WD10JPVX-75JC3T0   | 1 TB   | 4       | 405   | 94    | 0.16   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 1       | 284   | 4     | 0.16   |
| WDC       | WD5000BEVT-75A0RT0 | 500 GB | 1       | 511   | 8     | 0.16   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 1       | 56    | 0     | 0.15   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 1       | 55    | 0     | 0.15   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 3       | 55    | 0     | 0.15   |
| Hitachi   | HTS541040G9SA00    | 40 GB  | 1       | 330   | 5     | 0.15   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 1       | 52    | 0     | 0.14   |
| Seagate   | ST750LM022 HN-M... | 752 GB | 3       | 512   | 1138  | 0.14   |
| WDC       | WD3200BEKT-60V5T1  | 320 GB | 1       | 102   | 1     | 0.14   |
| WDC       | WD2503ABYZ-011FA0  | 256 GB | 1       | 50    | 0     | 0.14   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 3       | 50    | 0     | 0.14   |
| Seagate   | ST3250820AS        | 250 GB | 1       | 392   | 7     | 0.13   |
| WDC       | WD2500BEVT-08A23T1 | 250 GB | 1       | 97    | 1     | 0.13   |
| HGST      | HUS726060ALE610    | 6 TB   | 3       | 48    | 0     | 0.13   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 2       | 48    | 0     | 0.13   |
| Fujitsu   | MHZ2160BH G2       | 160 GB | 1       | 721   | 14    | 0.13   |
| WDC       | WD3200BUDT-63DPZY0 | 320 GB | 1       | 46    | 0     | 0.13   |
| Samsung   | HD322GJ            | 320 GB | 1       | 412   | 8     | 0.13   |
| WDC       | WD5000LUCT-63C26Y0 | 500 GB | 1       | 45    | 0     | 0.12   |
| WDC       | WD10SMRW-11Y43S0   | 1 TB   | 1       | 43    | 0     | 0.12   |
| WDC       | WD20EVDS-63T3B0    | 2 TB   | 1       | 385   | 8     | 0.12   |
| WDC       | WD3200BEVT-60ZCT1  | 320 GB | 2       | 237   | 5     | 0.12   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 2       | 42    | 0     | 0.12   |
| Hitachi   | HTS541612J9SA00    | 120 GB | 5       | 710   | 46    | 0.11   |
| Seagate   | ST2000NM000A-2J... | 2 TB   | 1       | 39    | 0     | 0.11   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 6       | 39    | 0     | 0.11   |
| WDC       | WD200EB-00BHF0     | 20 GB  | 1       | 273   | 6     | 0.11   |
| WDC       | WD120EFAX-68UNTN0  | 12 TB  | 2       | 38    | 0     | 0.11   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 1       | 38    | 0     | 0.11   |
| HGST      | HTS545032A7E380    | 320 GB | 4       | 402   | 12    | 0.11   |
| Seagate   | ST9500620NS        | 500 GB | 1       | 2829  | 73    | 0.10   |
| Samsung   | HM251JI            | 250 GB | 2       | 75    | 14    | 0.10   |
| Hitachi   | HTS541060G9SA00    | 64 GB  | 1       | 255   | 6     | 0.10   |
| WDC       | WD6400BEVT-22A0RT0 | 640 GB | 2       | 326   | 8     | 0.10   |
| WDC       | WD10SPZX-24Z10     | 1 TB   | 6       | 51    | 1     | 0.10   |
| WDC       | WD2002FYPS-01U1B1  | 2 TB   | 1       | 1621  | 45    | 0.10   |
| Fujitsu   | MHS2040AT D        | 40 GB  | 1       | 1334  | 37    | 0.10   |
| WDC       | WD4001FAEX-00MJRA0 | 4 TB   | 2       | 676   | 991   | 0.09   |
| Seagate   | ST1000DX001-1CM162 | 1 TB   | 1       | 671   | 19    | 0.09   |
| WDC       | WD5000AAKS-08V0A0  | 500 GB | 1       | 489   | 14    | 0.09   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 3       | 32    | 0     | 0.09   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 1       | 31    | 0     | 0.09   |
| WDC       | WD2500BEKT-00PVMT0 | 250 GB | 1       | 31    | 0     | 0.09   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 12      | 31    | 0     | 0.09   |
| Seagate   | ST250LT012-1DG141  | 250 GB | 1       | 30    | 0     | 0.08   |
| Seagate   | ST9320320AS        | 320 GB | 1       | 719   | 23    | 0.08   |
| Seagate   | ST9320325AS        | 320 GB | 5       | 626   | 272   | 0.08   |
| WDC       | WD6003FZBX-00K5WB0 | 6 TB   | 3       | 83    | 1     | 0.08   |
| Toshiba   | MK6475GSX          | 640 GB | 1       | 2340  | 83    | 0.08   |
| Maxtor    | STM3320613AS       | 320 GB | 1       | 1639  | 61    | 0.07   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 2       | 1598  | 597   | 0.07   |
| HPE       | MB0500EBNCR        | 500 GB | 1       | 49    | 1     | 0.07   |
| WDC       | WD1200JS-00MHB1    | 120 GB | 1       | 437   | 17    | 0.07   |
| Toshiba   | MK2552GSX          | 250 GB | 1       | 23    | 0     | 0.06   |
| Samsung   | HM320JI            | 320 GB | 3       | 208   | 9     | 0.06   |
| WDC       | WD800JD-00LSA0     | 80 GB  | 1       | 22    | 0     | 0.06   |
| Hitachi   | HTS725025A9A364    | 250 GB | 2       | 297   | 523   | 0.06   |
| Seagate   | ST20000NM007D-3... | 20 TB  | 2       | 22    | 0     | 0.06   |
| Maxtor    | 6L160M0            | 163 GB | 1       | 21    | 0     | 0.06   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 1       | 213   | 9     | 0.06   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 3       | 21    | 0     | 0.06   |
| HGST      | HUS726T6TALE6L1    | 6 TB   | 2       | 21    | 0     | 0.06   |
| WDC       | WD3200BEVE-00A0HT0 | 320 GB | 1       | 20    | 0     | 0.05   |
| WDC       | WD10EARX-22N0YB0   | 1 TB   | 1       | 175   | 8     | 0.05   |
| WDC       | WD30EZRZ-00WN9B0   | 3 TB   | 1       | 19    | 0     | 0.05   |
| Seagate   | ST500VT000-1DK142  | 500 GB | 2       | 520   | 443   | 0.05   |
| Seagate   | ST95005620AS       | 500 GB | 2       | 207   | 11    | 0.05   |
| Seagate   | ST8000DM004-2U9188 | 8 TB   | 1       | 17    | 0     | 0.05   |
| Seagate   | ST31500341AS       | 1.5 TB | 3       | 178   | 9     | 0.05   |
| Hitachi   | HTS548040M9AT00    | 40 GB  | 1       | 33    | 1     | 0.05   |
| Seagate   | ST3160812A         | 160 GB | 1       | 1810  | 107   | 0.05   |
| WDC       | WD80EDBZ-11B0ZA0   | 8 TB   | 1       | 16    | 0     | 0.05   |
| WDC       | WD7500LPCX-00KHST0 | 752 GB | 1       | 15    | 0     | 0.04   |
| WDC       | WD2500BEVT-80A23T0 | 250 GB | 1       | 425   | 26    | 0.04   |
| WDC       | WD40EFZX-68AWUN0   | 4 TB   | 2       | 15    | 0     | 0.04   |
| Toshiba   | HDWD105            | 500 GB | 2       | 1701  | 286   | 0.04   |
| HGST      | HUS726040ALA610    | 4 TB   | 1       | 1058  | 78    | 0.04   |
| WDC       | WD1600BEVT-80A23T0 | 160 GB | 2       | 50    | 5     | 0.03   |
| WDC       | WD10JPVX-60JC3T0   | 1 TB   | 2       | 321   | 140   | 0.03   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 11      | 339   | 1087  | 0.03   |
| WDC       | WD1600BPVT-11JJ5T0 | 160 GB | 1       | 11    | 0     | 0.03   |
| Seagate   | ST1000LM025 HN-... | 1 TB   | 1       | 117   | 9     | 0.03   |
| WDC       | WD3200AAKS-00UU3A0 | 320 GB | 1       | 103   | 8     | 0.03   |
| Samsung   | HM080HI            | 80 GB  | 1       | 627   | 56    | 0.03   |
| Seagate   | ST18000NM000J-2... | 18 TB  | 16      | 10    | 0     | 0.03   |
| Seagate   | ST9250320AS        | 250 GB | 1       | 241   | 22    | 0.03   |
| WDC       | WD1600BEKT-08PVMT1 | 160 GB | 2       | 204   | 172   | 0.03   |
| Samsung   | HS082HB            | 80 GB  | 1       | 273   | 26    | 0.03   |
| Hitachi   | HTS543225A7A384    | 250 GB | 1       | 237   | 23    | 0.03   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 1       | 80    | 8     | 0.02   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 2       | 8     | 0     | 0.02   |
| Toshiba   | MK3255GSXF         | 320 GB | 1       | 8     | 0     | 0.02   |
| WDC       | WD1600BEVS-60RST0  | 160 GB | 1       | 164   | 18    | 0.02   |
| WDC       | WD100EZAZ-11TDBA0  | 10 TB  | 1       | 8     | 0     | 0.02   |
| Toshiba   | MQ03UBB300         | 3 TB   | 1       | 8     | 0     | 0.02   |
| Hitachi   | HTS543212L9A300    | 120 GB | 2       | 1802  | 550   | 0.02   |
| Toshiba   | MK5061GSY          | 500 GB | 1       | 7     | 0     | 0.02   |
| Hitachi   | HDP725016GLA380    | 160 GB | 1       | 1804  | 250   | 0.02   |
| Samsung   | HM321HI            | 320 GB | 3       | 69    | 289   | 0.02   |
| Seagate   | ST32500NSSUN250G   | 250 GB | 2       | 6     | 0     | 0.02   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 1       | 2670  | 395   | 0.02   |
| WDC       | WD2500BEVT-60A23T0 | 250 GB | 1       | 250   | 37    | 0.02   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 4       | 6     | 0     | 0.02   |
| Maxtor    | 6Y080M0            | 82 GB  | 1       | 31    | 4     | 0.02   |
| WDC       | WD1600BEVS-08VAT1  | 160 GB | 1       | 591   | 96    | 0.02   |
| Toshiba   | MK5061GSYN         | 500 GB | 3       | 15    | 20    | 0.02   |
| Toshiba   | MQ02ABF050H-SSH... | 500 GB | 1       | 540   | 93    | 0.02   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 2       | 2203  | 676   | 0.02   |
| Seagate   | ST380211AS         | 80 GB  | 1       | 1418  | 277   | 0.01   |
| Toshiba   | MK8025GAS          | 80 GB  | 1       | 5     | 0     | 0.01   |
| WDC       | WD3200BEVT-60ZCT0  | 320 GB | 1       | 133   | 29    | 0.01   |
| WDC       | WD3200LPVX-75V0TT0 | 320 GB | 1       | 490   | 115   | 0.01   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 1       | 1809  | 456   | 0.01   |
| Seagate   | ST3160815A         | 160 GB | 1       | 4054  | 1048  | 0.01   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 16      | 3     | 0     | 0.01   |
| Toshiba   | MK3256GSY          | 320 GB | 1       | 3     | 0     | 0.01   |
| Apple     | HDD HTS547550A9... | 500 GB | 1       | 96    | 28    | 0.01   |
| WDC       | WD5000AAKS-60WWPA0 | 500 GB | 1       | 798   | 241   | 0.01   |
| Hitachi   | HTS543216L9A300    | 160 GB | 1       | 1644  | 522   | 0.01   |
| Seagate   | ST3200822AS        | 200 GB | 1       | 3219  | 1105  | 0.01   |
| Toshiba   | MK3261GSY          | 320 GB | 1       | 2     | 0     | 0.01   |
| Toshiba   | MQ01ABD100V        | 1 TB   | 1       | 2     | 0     | 0.01   |
| Seagate   | ST2000DL001-9VT156 | 2 TB   | 1       | 2429  | 1010  | 0.01   |
| Toshiba   | MK2018GAP          | 20 GB  | 1       | 126   | 55    | 0.01   |
| WDC       | WD1600BEKT-66F3T2  | 160 GB | 2       | 2270  | 1016  | 0.01   |
| Hitachi   | HTS541616J9SA00    | 160 GB | 1       | 527   | 235   | 0.01   |
| WDC       | WD181KFGX-68AFPN0  | 18 TB  | 1       | 2     | 0     | 0.01   |
| Samsung   | HD321KJ            | 320 GB | 1       | 2154  | 1016  | 0.01   |
| HGST      | HTS725025A7E630    | 250 GB | 1       | 43    | 20    | 0.01   |
| Seagate   | ST3500514NS        | 500 GB | 1       | 205   | 103   | 0.01   |
| Maxtor    | 6Y080P0            | 82 GB  | 3       | 15    | 413   | 0.01   |
| Seagate   | ST31000333AS       | 1 TB   | 1       | 316   | 164   | 0.01   |
| Seagate   | ST320DM000-1BD14C  | 320 GB | 1       | 1890  | 1006  | 0.01   |
| WDC       | WD40EZAZ-00SF3B0   | 4 TB   | 1       | 1     | 0     | 0.01   |
| Toshiba   | MK2556GSY          | 250 GB | 1       | 1     | 0     | 0.00   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 1       | 1     | 0     | 0.00   |
| Seagate   | ST2000DM001-1E6164 | 2 TB   | 1       | 1542  | 904   | 0.00   |
| HGST      | HUS726060ALE614    | 6 TB   | 4       | 1     | 0     | 0.00   |
| WDC       | WD6400AARS-00Y5B1  | 640 GB | 1       | 2549  | 1904  | 0.00   |
| Samsung   | SP2004C            | 200 GB | 1       | 1339  | 1014  | 0.00   |
| WDC       | WD2005FBYZ-01YCBB3 | 2 TB   | 2       | 1     | 0     | 0.00   |
| WDC       | WD800JD-55MUA1     | 80 GB  | 1       | 609   | 481   | 0.00   |
| Toshiba   | MK7559GSXF         | 752 GB | 1       | 1450  | 1185  | 0.00   |
| WDC       | WD2500JS-22NCB1    | 250 GB | 1       | 1197  | 1038  | 0.00   |
| WDC       | WD1600BEVS-00UST0  | 160 GB | 1       | 87    | 76    | 0.00   |
| Seagate   | ST9640320AS        | 640 GB | 2       | 1168  | 1039  | 0.00   |
| Toshiba   | HDWG480            | 8 TB   | 2       | 1     | 0     | 0.00   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 1       | 1094  | 1007  | 0.00   |
| Toshiba   | MK1252GSX          | 120 GB | 1       | 8     | 7     | 0.00   |
| WDC       | WD1200BEVS-07LAT0  | 120 GB | 1       | 150   | 164   | 0.00   |
| Seagate   | ST980816AS         | 80 GB  | 1       | 446   | 494   | 0.00   |
| Hitachi   | HDS723015BLA642    | 1.5 TB | 1       | 902   | 1016  | 0.00   |
| Toshiba   | MK3261GSYN         | 320 GB | 3       | 6     | 125   | 0.00   |
| Seagate   | ST320LM010-1KJ15C  | 320 GB | 1       | 859   | 1010  | 0.00   |
| Seagate   | ST3160310CS        | 160 GB | 1       | 469   | 609   | 0.00   |
| Hitachi   | HCC543225A7A380    | 250 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | HD642JJ            | 640 GB | 2       | 1044  | 1351  | 0.00   |
| Seagate   | ST9160827AS        | 160 GB | 1       | 657   | 1010  | 0.00   |
| Seagate   | ST9160314AS        | 160 GB | 1       | 684   | 1062  | 0.00   |
| Hitachi   | HTS723216L9A360    | 160 GB | 1       | 646   | 1013  | 0.00   |
| Maxtor    | STM3160815AS       | 160 GB | 1       | 603   | 959   | 0.00   |
| Hitachi   | HTS725050A9A364    | 500 GB | 1       | 862   | 1522  | 0.00   |
| WDC       | WD10EADS-00M2B0    | 1 TB   | 1       | 849   | 1554  | 0.00   |
| WDC       | WD8003FFBX-68B9AN0 | 8 TB   | 4       | 0     | 0     | 0.00   |
| Fujitsu   | MHW2160BH          | 160 GB | 1       | 475   | 957   | 0.00   |
| Samsung   | HM500LI            | 500 GB | 1       | 1476  | 3036  | 0.00   |
| Hitachi   | HTS545050B9A300    | 500 GB | 1       | 458   | 1045  | 0.00   |
| Seagate   | ST320LT012-9WS14C  | 320 GB | 1       | 761   | 2087  | 0.00   |
| Hitachi   | HTS725032A7E630    | 320 GB | 1       | 348   | 1025  | 0.00   |
| Seagate   | ST9160412AS        | 160 GB | 1       | 313   | 1009  | 0.00   |
| Seagate   | ST9320325ASG       | 320 GB | 1       | 615   | 2012  | 0.00   |
| Seagate   | ST1000NM004A-2M... | 1 TB   | 1       | 0     | 0     | 0.00   |
| Hitachi   | HTS725032A9A364    | 320 GB | 1       | 259   | 1023  | 0.00   |
| Seagate   | ST1000NM000A       | 1 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD5000B            | 500 GB | 1       | 252   | 1011  | 0.00   |
| Seagate   | ST3160215AS        | 160 GB | 1       | 551   | 2350  | 0.00   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 10      | 0     | 0     | 0.00   |
| Toshiba   | MK2555GSXF         | 250 GB | 1       | 294   | 1456  | 0.00   |
| Seagate   | ST9160821AS        | 160 GB | 1       | 376   | 2103  | 0.00   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | HM121HI            | 120 GB | 1       | 501   | 3029  | 0.00   |
| Hitachi   | DK23AA-12          | 12 GB  | 1       | 4     | 31    | 0.00   |
| Samsung   | HD252HJ            | 250 GB | 1       | 173   | 1520  | 0.00   |
| Samsung   | HD082GJ            | 80 GB  | 1       | 109   | 1015  | 0.00   |
| HGST      | HTS541010A7E630    | 1 TB   | 1       | 96    | 1023  | 0.00   |
| Fujitsu   | MHV2120BH PL       | 120 GB | 1       | 0     | 0     | 0.00   |
| Hitachi   | HCS5C1050CLA382    | 500 GB | 1       | 9     | 142   | 0.00   |
| Maxtor    | 6Y160M0            | 160 GB | 1       | 7     | 149   | 0.00   |
| Maxtor    | 6E040L0            | 41 GB  | 1       | 20    | 1133  | 0.00   |
| Samsung   | HM250JI            | 250 GB | 1       | 16    | 1010  | 0.00   |
| Toshiba   | MK1059GSM          | 1 TB   | 1       | 8     | 558   | 0.00   |
| Hitachi   | HTS721060G9AT00    | 64 GB  | 1       | 0     | 37    | 0.00   |
| Samsung   | HM251JX            | 250 GB | 1       | 0     | 92    | 0.00   |
| Toshiba   | MK3276GSX          | 320 GB | 1       | 2     | 1008  | 0.00   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| Seagate   | Barracuda ATA V        | 1      | 1       | 5214  | 0     | 14.29  |
| Hitachi   | Deskstar 7K500         | 1      | 1       | 3763  | 0     | 10.31  |
| Hitachi   | Sun Internal           | 1      | 2       | 2785  | 0     | 7.63   |
| Seagate   | Barracuda Green        | 1      | 1       | 2746  | 0     | 7.52   |
| Seagate   | Constellation ES.2 ... | 2      | 2       | 2666  | 0     | 7.31   |
| WDC       | RE3                    | 8      | 14      | 2741  | 1     | 6.49   |
| Seagate   | Momentus Xt            | 1      | 1       | 2334  | 0     | 6.40   |
| Hitachi   | Deskstar 7K2000        | 1      | 2       | 2241  | 0     | 6.14   |
| Hitachi   | Deskstar 7K80          | 1      | 1       | 2086  | 0     | 5.72   |
| Hitachi   | Deskstar 5K4000        | 1      | 21      | 2076  | 0     | 5.69   |
| Seagate   | Barracuda XT           | 2      | 7       | 2029  | 0     | 5.56   |
| Hitachi   | Deskstar 7K1000.B      | 3      | 8       | 2706  | 2     | 5.44   |
| HP        | Proliant HardDrive     | 4      | 10      | 2737  | 1     | 5.35   |
| Hitachi   | Deskstar 5K3000        | 1      | 18      | 2020  | 2     | 5.23   |
| Seagate   | DB35.3                 | 1      | 1       | 1863  | 0     | 5.11   |
| Seagate   | Barracuda 7200.8       | 2      | 2       | 2924  | 4     | 4.77   |
| Hitachi   | Ultrastar 7K3000       | 3      | 19      | 1799  | 107   | 4.73   |
| Hitachi   | Ultrastar A7K1000      | 2      | 3       | 2579  | 1     | 4.73   |
| Seagate   | Desktop HDD            | 1      | 2       | 1714  | 0     | 4.70   |
| WDC       | Caviar Black           | 15     | 48      | 1973  | 27    | 4.59   |
| HGST      | Ultrastar 7K4000       | 3      | 12      | 1647  | 0     | 4.51   |
| Toshiba   | 2.5" HDD MK..76GSX     | 1      | 1       | 1634  | 0     | 4.48   |
| Samsung   | SpinPoint F3           | 2      | 10      | 1958  | 1     | 4.44   |
| Maxtor    | DiamondMax 10 (SATA... | 2      | 2       | 1537  | 0     | 4.21   |
| Samsung   | SpinPoint F4 EG (AF)   | 1      | 18      | 2043  | 7     | 4.18   |
| Seagate   | Barracuda ES           | 4      | 10      | 2024  | 209   | 4.18   |
| Maxtor    | DiamondMax Plus D740X  | 1      | 3       | 2093  | 2     | 4.15   |
| Seagate   | SpinPoint F4 EG (AF)   | 1      | 2       | 1504  | 0     | 4.12   |
| WDC       | Protege                | 2      | 2       | 1616  | 3     | 4.11   |
| Hitachi   | Deskstar E7K1000       | 1      | 3       | 3419  | 4     | 4.09   |
| HP        | Seagate Constellati... | 1      | 7       | 1962  | 4     | 4.08   |
| Seagate   | Desktop HDD.15         | 6      | 48      | 1570  | 23    | 4.07   |
| WDC       | AV                     | 3      | 5       | 1479  | 0     | 4.05   |
| Seagate   | NAS HDD                | 4      | 18      | 1556  | 2     | 4.01   |
| WDC       | Caviar SE              | 25     | 36      | 1925  | 44    | 3.98   |
| Seagate   | Constellation CS       | 2      | 5       | 1808  | 23    | 3.98   |
| WDC       | Green                  | 18     | 58      | 1600  | 22    | 3.96   |
| HGST      | Deskstar NAS           | 6      | 40      | 1552  | 21    | 3.90   |
| Hitachi   | Deskstar 7K1000        | 2      | 10      | 1951  | 1     | 3.84   |
| WDC       | VelociRaptor           | 7      | 12      | 1396  | 1     | 3.71   |
| Hitachi   | Deskstar 7K160         | 2      | 2       | 1343  | 0     | 3.68   |
| Hitachi   | Ultrastar A7K2000      | 4      | 24      | 1755  | 39    | 3.63   |
| WDC       | Se                     | 3      | 4       | 1321  | 0     | 3.62   |
| WDC       | Caviar                 | 5      | 6       | 2283  | 120   | 3.61   |
| WDC       | Caviar SE16            | 1      | 1       | 1317  | 0     | 3.61   |
| HGST      | Ultrastar He8          | 2      | 2       | 1299  | 0     | 3.56   |
| Seagate   | Momentus 7200.5        | 1      | 1       | 1283  | 0     | 3.52   |
| WDC       | RE4                    | 13     | 35      | 1331  | 1     | 3.45   |
| Seagate   | Terascale              | 2      | 4       | 1216  | 0     | 3.33   |
| Toshiba   | 3.5" HDD E300          | 1      | 1       | 1207  | 0     | 3.31   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 2      | 15      | 1194  | 0     | 3.27   |
| Hitachi   | Deskstar T7K500        | 2      | 3       | 1187  | 0     | 3.25   |
| WDC       | Unknown                | 1      | 1       | 1179  | 0     | 3.23   |
| WDC       | Caviar Green           | 20     | 39      | 1820  | 204   | 3.19   |
| Seagate   | Pipeline HD 5900.2     | 4      | 19      | 1263  | 51    | 3.12   |
| Hitachi   | Deskstar 5K1000        | 1      | 1       | 1122  | 0     | 3.08   |
| Samsung   | SpinPoint S250         | 1      | 1       | 1084  | 0     | 2.97   |
| Samsung   | SpinPoint T166         | 3      | 10      | 2206  | 205   | 2.97   |
| Toshiba   | 2.5" HDD MQ01UBB       | 1      | 1       | 1067  | 0     | 2.93   |
| WDC       | RE                     | 7      | 19      | 1741  | 16    | 2.86   |
| Toshiba   | 2.5" HDD MQ01ABD..H    | 1      | 2       | 1041  | 0     | 2.85   |
| WDC       | Raptor                 | 3      | 3       | 1098  | 2     | 2.80   |
| Seagate   | Archive HDD            | 1      | 6       | 1317  | 169   | 2.79   |
| Seagate   | Momentus 7200.3        | 3      | 4       | 1110  | 2     | 2.71   |
| WDC       | Scorpio Black          | 19     | 31      | 1163  | 77    | 2.71   |
| WDC       | Caviar Blue            | 43     | 62      | 1446  | 46    | 2.65   |
| Toshiba   | 3.5" MG04ACA Enterp... | 2      | 4       | 959   | 0     | 2.63   |
| WDC       | Red                    | 23     | 353     | 1148  | 16    | 2.63   |
| Hitachi   | Travelstar 7K750       | 1      | 4       | 1013  | 32    | 2.62   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 1       | 953   | 0     | 2.61   |
| Samsung   | SpinPoint F1 DT        | 9      | 28      | 1411  | 186   | 2.58   |
| Seagate   | Surveillance           | 3      | 4       | 932   | 0     | 2.55   |
| CLOVER    | Hightech Utania        | 1      | 1       | 928   | 0     | 2.54   |
| Toshiba   | 2.5" HDD MQ04UBD       | 1      | 1       | 906   | 0     | 2.48   |
| Seagate   | Constellation ES.3     | 4      | 21      | 1417  | 386   | 2.44   |
| Seagate   | Barracuda 7200.7 an... | 7      | 14      | 1434  | 81    | 2.39   |
| Maxtor    | DiamondMax 21          | 3      | 6       | 1019  | 161   | 2.38   |
| Samsung   | SpinPoint F2 EG        | 3      | 11      | 1277  | 289   | 2.36   |
| Seagate   | U6                     | 1      | 1       | 2579  | 2     | 2.36   |
| Toshiba   | 3.5" MD04ACA Enterp... | 1      | 3       | 893   | 3     | 2.32   |
| Seagate   | Exos X14               | 1      | 2       | 840   | 0     | 2.30   |
| WDC       | RE2                    | 2      | 2       | 835   | 0     | 2.29   |
| WDC       | Gold                   | 8      | 21      | 837   | 18    | 2.27   |
| Hitachi   | CinemaStar Z5K320      | 2      | 2       | 825   | 0     | 2.26   |
| Seagate   | Barracuda 7200.9       | 10     | 13      | 1481  | 131   | 2.24   |
| Seagate   | Barracuda Green (AF)   | 4      | 16      | 1526  | 271   | 2.23   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 69      | 905   | 35    | 2.21   |
| Lenovo    | RE                     | 1      | 4       | 802   | 0     | 2.20   |
| Hitachi   | Deskstar 7K1000.C      | 7      | 15      | 1370  | 219   | 2.18   |
| HPE       | Proliant HardDrive     | 2      | 12      | 792   | 0     | 2.17   |
| HP        | 250GB SATA disk VB0... | 1      | 1       | 2348  | 2     | 2.14   |
| Seagate   | Constellation ES (S... | 3      | 7       | 1912  | 10    | 2.09   |
| Seagate   | Barracuda 3.5          | 2      | 13      | 1055  | 143   | 2.09   |
| Seagate   | Skyhawk                | 2      | 9       | 841   | 1     | 2.03   |
| Seagate   | Barracuda 7200.14 (AF) | 20     | 167     | 993   | 141   | 2.02   |
| Seagate   | Barracuda 7200.12      | 11     | 80      | 1196  | 140   | 1.92   |
| Hitachi   | Sun                    | 1      | 1       | 696   | 0     | 1.91   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 1      | 1       | 692   | 0     | 1.90   |
| Seagate   | Exos 7E2               | 1      | 1       | 684   | 0     | 1.88   |
| MaxDig... | Unknown                | 1      | 1       | 681   | 0     | 1.87   |
| Samsung   | SpinPoint M7           | 4      | 12      | 759   | 26    | 1.84   |
| Seagate   | IronWolf Pro           | 4      | 10      | 745   | 1     | 1.84   |
| WDC       | Purple                 | 11     | 20      | 777   | 1     | 1.79   |
| Samsung   | SpinPoint P80 SD       | 2      | 2       | 637   | 0     | 1.75   |
| WDC       | Blue                   | 68     | 197     | 762   | 12    | 1.71   |
| Seagate   | Barracuda LP           | 3      | 10      | 1150  | 217   | 1.71   |
| Toshiba   | X300                   | 4      | 15      | 706   | 3     | 1.69   |
| Apple     | Momentus               | 1      | 1       | 617   | 0     | 1.69   |
| Hitachi   | Deskstar 7K4000        | 1      | 1       | 614   | 0     | 1.68   |
| Seagate   | Exos X12               | 1      | 5       | 613   | 0     | 1.68   |
| Seagate   | Barracuda 7200.10      | 15     | 42      | 1249  | 285   | 1.67   |
| ExcelStor | Jupiter                | 2      | 4       | 1009  | 8     | 1.64   |
| WDC       | Ultrastar He10/12      | 3      | 14      | 598   | 0     | 1.64   |
| Hitachi   | Travelstar 5K250       | 4      | 6       | 765   | 2     | 1.63   |
| Toshiba   | Unknown                | 4      | 5       | 593   | 0     | 1.63   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 1       | 592   | 0     | 1.62   |
| Hitachi   | Deskstar 7K3000        | 3      | 6       | 1475  | 193   | 1.59   |
| Samsung   | SpinPoint F3 EG        | 2      | 2       | 580   | 0     | 1.59   |
| Seagate   | Constellation.2 (SATA) | 2      | 3       | 1508  | 25    | 1.58   |
| Samsung   | SpinPoint MP5          | 1      | 1       | 571   | 0     | 1.57   |
| WDC       | Red Pro                | 10     | 33      | 593   | 62    | 1.50   |
| HPE       | WDC Enterprise         | 2      | 7       | 560   | 2     | 1.44   |
| IBM       | Travelstar 6GN         | 1      | 1       | 522   | 0     | 1.43   |
| Hitachi   | Deskstar P7K500        | 3      | 5       | 1195  | 59    | 1.39   |
| Hitachi   | Travelstar Z5K320      | 3      | 8       | 665   | 271   | 1.33   |
| Samsung   | SpinPoint S166         | 2      | 5       | 507   | 203   | 1.33   |
| WDC       | Black Mobile           | 13     | 24      | 563   | 1     | 1.32   |
| Maxtor    | DiamondMax 8s          | 1      | 1       | 482   | 0     | 1.32   |
| Hitachi   | Travelstar 5K500.B     | 8      | 19      | 630   | 320   | 1.31   |
| HGST      | Travelstar 7K1000      | 1      | 21      | 529   | 147   | 1.31   |
| Toshiba   | 2.5" HDD MQ01UBD       | 1      | 1       | 944   | 1     | 1.29   |
| Seagate   | SpinPoint M9T          | 1      | 6       | 470   | 0     | 1.29   |
| HGST      | Travelstar 5K1000      | 1      | 14      | 544   | 295   | 1.28   |
| Samsung   | SpinPoint P120         | 3      | 3       | 1675  | 342   | 1.27   |
| WDC       | HGST Ultrastar He10    | 2      | 17      | 458   | 0     | 1.25   |
| WDC       | Elements / My Passport | 13     | 22      | 570   | 49    | 1.25   |
| Seagate   | Barracuda 7200.11      | 4      | 9       | 827   | 24    | 1.24   |
| Toshiba   | N300/MN NAS HDD        | 3      | 13      | 439   | 0     | 1.20   |
| Fujitsu   | MJA BH                 | 5      | 7       | 434   | 0     | 1.19   |
| Seagate   | Laptop SSHD            | 5      | 14      | 520   | 76    | 1.18   |
| Hitachi   | Travelstar 5K100       | 4      | 4       | 615   | 3     | 1.17   |
| Hitachi   | Ultrastar 7K4000       | 2      | 19      | 431   | 1     | 1.17   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 10      | 478   | 100   | 1.16   |
| HGST      | Ultrastar HC310/320    | 1      | 8       | 414   | 0     | 1.13   |
| Seagate   | SpinPoint M8 (AF)      | 4      | 43      | 570   | 105   | 1.12   |
| HGST      | Ultrastar 7K6000       | 8      | 17      | 462   | 5     | 1.10   |
| HGST      | Ultrastar 7K2          | 3      | 6       | 493   | 3     | 1.09   |
| WDC       | Scorpio Blue           | 55     | 95      | 496   | 29    | 1.05   |
| WDC       | Black                  | 9      | 23      | 447   | 87    | 1.03   |
| Seagate   | Video 2.5              | 2      | 3       | 708   | 296   | 1.02   |
| WDC       | AV-GP                  | 7      | 9       | 780   | 3     | 0.97   |
| Seagate   | BarraCuda 3.5          | 10     | 89      | 394   | 33    | 0.96   |
| Hitachi   | Travelstar 7K320       | 3      | 3       | 564   | 338   | 0.96   |
| Toshiba   | Toshiba Client HDD     | 1      | 2       | 345   | 0     | 0.95   |
| HGST      | Travelstar Z7K500      | 5      | 30      | 663   | 354   | 0.95   |
| Fujitsu   | MHY BH                 | 3      | 4       | 343   | 0     | 0.94   |
| Toshiba   | 2.5" HDD               | 5      | 6       | 358   | 10    | 0.93   |
| Seagate   | Momentus 7200.4        | 6      | 23      | 718   | 669   | 0.92   |
| Toshiba   | 2.5" HDD MK..46GSX     | 1      | 2       | 604   | 17    | 0.92   |
| Fujitsu   | MHT                    | 2      | 2       | 334   | 0     | 0.92   |
| Hitachi   | Travelstar 7K500       | 4      | 5       | 668   | 718   | 0.91   |
| Seagate   | Barracuda Compute      | 1      | 26      | 333   | 0     | 0.91   |
| Toshiba   | 2.5" HDD MK..59GSXP    | 1      | 1       | 326   | 0     | 0.89   |
| Seagate   | Barracuda 2.5 5400     | 5      | 44      | 352   | 39    | 0.89   |
| MediaMax  | WL2000                 | 1      | 3       | 697   | 6     | 0.89   |
| Toshiba   | 3.5" DT01ABA Deskto... | 1      | 3       | 622   | 3     | 0.88   |
| Fujitsu   | MHW BH                 | 2      | 2       | 558   | 479   | 0.88   |
| Seagate   | IronWolf               | 10     | 77      | 332   | 1     | 0.88   |
| Toshiba   | 2.5" HDD MK..37GSX     | 1      | 2       | 813   | 1     | 0.87   |
| Seagate   | Enterprise Capacity... | 5      | 9       | 317   | 0     | 0.87   |
| Hitachi   | Travelstar Z7K320      | 2      | 8       | 849   | 405   | 0.84   |
| Toshiba   | P300                   | 4      | 32      | 416   | 19    | 0.83   |
| Apple     | Travelstar 5K1000      | 2      | 4       | 502   | 1     | 0.82   |
| Toshiba   | 3.5" HDD DT01ACA       | 1      | 1       | 298   | 0     | 0.82   |
| Toshiba   | N300 NAS HDD           | 1      | 9       | 298   | 0     | 0.82   |
| Seagate   | Momentus 7200.1        | 1      | 1       | 1419  | 4     | 0.78   |
| Fujitsu   | MHV                    | 2      | 2       | 276   | 0     | 0.76   |
| WDC       | Blue Mobile            | 35     | 93      | 316   | 28    | 0.74   |
| Hitachi   | Travelstar Z7K500      | 2      | 2       | 442   | 513   | 0.73   |
| Toshiba   | 2.5" HDD MQ01ABF       | 2      | 3       | 265   | 0     | 0.73   |
| Hitachi   | Travelstar 5K750       | 2      | 9       | 421   | 245   | 0.71   |
| Toshiba   | 2.5" HDD MQ02ABD..H    | 1      | 3       | 368   | 23    | 0.70   |
| HGST      | Travelstar Z5K500      | 4      | 16      | 420   | 68    | 0.68   |
| WDC       | Blue SSHD              | 1      | 1       | 245   | 0     | 0.67   |
| Seagate   | Momentus 5400.2        | 2      | 6       | 255   | 1     | 0.67   |
| Samsung   | SpinPoint P80          | 1      | 1       | 234   | 0     | 0.64   |
| Seagate   | FireCuda 2.5           | 3      | 9       | 330   | 476   | 0.64   |
| Apple     | Barracuda 7200.12      | 1      | 1       | 232   | 0     | 0.64   |
| Seagate   | Desktop SSHD           | 2      | 2       | 538   | 10    | 0.60   |
| Seagate   | Momentus 5400.6        | 8      | 31      | 587   | 315   | 0.60   |
| Seagate   | Momentus 5400.4        | 2      | 5       | 523   | 209   | 0.59   |
| Toshiba   | 2.5" HDD MQ01ABD       | 5      | 42      | 368   | 162   | 0.59   |
| Seagate   | Barracuda ES.2         | 2      | 2       | 2115  | 9     | 0.56   |
| Toshiba   | 2.5" HDD MQ04UBB       | 1      | 1       | 201   | 0     | 0.55   |
| Samsung   | SpinPoint M8 (AF)      | 2      | 3       | 200   | 0     | 0.55   |
| Toshiba   | 2.5" HDD MK..65GSX     | 3      | 5       | 328   | 3     | 0.55   |
| Toshiba   | 2.5" HDD MK..63GSX     | 1      | 1       | 1135  | 5     | 0.52   |
| Toshiba   | 2.5" HDD MQ03UBB       | 2      | 3       | 182   | 0     | 0.50   |
| Hitachi   | Travelstar Z5K500      | 1      | 5       | 262   | 73    | 0.48   |
| Fujitsu   | MHZ BH                 | 4      | 4       | 488   | 6     | 0.46   |
| HGST      | Travelstar Z5K1000     | 3      | 9       | 200   | 227   | 0.46   |
| Seagate   | Momentus 5400.3        | 4      | 6       | 393   | 353   | 0.45   |
| Hitachi   | Travelstar 7K100       | 3      | 3       | 551   | 14    | 0.45   |
| Toshiba   | 2.5" HDD MK..55GSX     | 1      | 1       | 160   | 0     | 0.44   |
| Seagate   | Momentus 5400.5        | 4      | 4       | 976   | 14    | 0.43   |
| Seagate   | Momentus 5400.7 (AF)   | 1      | 2       | 152   | 0     | 0.42   |
| Hitachi   | Travelstar 5K320       | 6      | 9       | 1174  | 314   | 0.41   |
| Seagate   | Mobile HDD             | 2      | 34      | 176   | 65    | 0.39   |
| Seagate   | Video 3.5 HDD          | 3      | 5       | 749   | 93    | 0.39   |
| Seagate   | Laptop HDD             | 7      | 41      | 467   | 667   | 0.37   |
| Toshiba   | 2.5" HDD MK..55GSX     | 4      | 6       | 499   | 477   | 0.37   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 17      | 203   | 120   | 0.35   |
| WDC       | Red Plus               | 2      | 4       | 124   | 0     | 0.34   |
| WDC       | White Label            | 3      | 11      | 122   | 0     | 0.33   |
| Hitachi   | Travelstar 5K160       | 4      | 12      | 636   | 43    | 0.33   |
| WDC       | RE4-GP                 | 3      | 5       | 1834  | 282   | 0.33   |
| Apple     | HGST Travelstar Z5K500 | 1      | 4       | 157   | 6     | 0.33   |
| Samsung   | SpinPoint F4           | 2      | 2       | 843   | 7     | 0.31   |
| Seagate   | Constellation          | 1      | 2       | 221   | 48    | 0.31   |
| Hitachi   | Travelstar 7K200       | 2      | 2       | 280   | 2     | 0.30   |
| Apple     | HGST Travelstar 5K750  | 2      | 2       | 156   | 14    | 0.30   |
| WDC       | IU CB500               | 1      | 1       | 106   | 0     | 0.29   |
| Seagate   | Exos X16               | 1      | 6       | 105   | 0     | 0.29   |
| Seagate   | Barracuda Pro Compute  | 1      | 9       | 160   | 1     | 0.28   |
| Hitachi   | Travelstar 4K120       | 1      | 1       | 1338  | 12    | 0.28   |
| HGST      | Ultrastar He10         | 1      | 2       | 102   | 0     | 0.28   |
| WDC       | Internal Use HDD       | 2      | 3       | 102   | 0     | 0.28   |
| Seagate   | Momentus 7200.2        | 1      | 1       | 93    | 0     | 0.26   |
| Seagate   | Ultra Mobile HDD       | 1      | 1       | 89    | 0     | 0.24   |
| Seagate   | Unknown                | 1      | 1       | 87    | 0     | 0.24   |
| HGST      | MegaScale 4000         | 2      | 19      | 83    | 0     | 0.23   |
| Toshiba   | 2.5" HDD MK..34GSX     | 1      | 1       | 416   | 4     | 0.23   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 5      | 9       | 85    | 48    | 0.22   |
| WDC       | Ultrastar DC HC530     | 1      | 1       | 79    | 0     | 0.22   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 12      | 98    | 1     | 0.21   |
| Toshiba   | Toshiba Enterprise     | 1      | 1       | 72    | 0     | 0.20   |
| Toshiba   | 1.8" HDD               | 1      | 1       | 426   | 5     | 0.19   |
| Hitachi   | CinemaStar C5K500      | 1      | 1       | 70    | 0     | 0.19   |
| Toshiba   | 2.5" HDD MK..75GSX     | 2      | 2       | 1472  | 44    | 0.18   |
| Toshiba   | MG09ACA Enterprise ... | 1      | 2       | 60    | 0     | 0.17   |
| Seagate   | Momentus Thin          | 1      | 8       | 461   | 765   | 0.16   |
| Seagate   | Constellation ES (S... | 2      | 2       | 153   | 52    | 0.14   |
| Samsung   | SpinPoint M5           | 3      | 8       | 311   | 540   | 0.12   |
| Toshiba   | 2.5" HDD MQ02ABF..H    | 2      | 3       | 221   | 31    | 0.12   |
| Seagate   | Exos 7E8               | 4      | 5       | 40    | 0     | 0.11   |
| Fujitsu   | MHS AT                 | 1      | 1       | 1334  | 37    | 0.10   |
| Maxtor    | DiamondMax 22          | 1      | 1       | 1639  | 61    | 0.07   |
| Samsung   | SpinPoint M6           | 3      | 6       | 375   | 516   | 0.07   |
| Seagate   | Exos X20               | 1      | 2       | 22    | 0     | 0.06   |
| Maxtor    | DiamondMax 10 (ATA/... | 1      | 1       | 21    | 0     | 0.06   |
| HGST      | Ultrastar DC HC310     | 1      | 2       | 21    | 0     | 0.06   |
| WDC       | Scorpio Blue EIDE      | 1      | 1       | 20    | 0     | 0.05   |
| Seagate   | Momentus XT            | 1      | 2       | 207   | 11    | 0.05   |
| Hitachi   | Travelstar 5K80        | 1      | 1       | 33    | 1     | 0.05   |
| Toshiba   | 2.5" HDD MK..52GSX     | 2      | 2       | 15    | 4     | 0.03   |
| Seagate   | SpinPoint M8U (USB)    | 1      | 1       | 117   | 9     | 0.03   |
| Samsung   | SpinPoint M40/60/80    | 1      | 1       | 627   | 56    | 0.03   |
| Seagate   | Exos X18               | 1      | 16      | 10    | 0     | 0.03   |
| Samsung   | SpinPoint N2           | 1      | 1       | 273   | 26    | 0.03   |
| Samsung   | SpinPoint M7E (AF)     | 1      | 3       | 69    | 289   | 0.02   |
| Toshiba   | MG07ACA Enterprise ... | 1      | 4       | 6     | 0     | 0.02   |
| Toshiba   | 2.5" HDD MK..56GSY     | 2      | 2       | 2     | 0     | 0.01   |
| Maxtor    | DiamondMax Plus 9      | 3      | 5       | 17    | 279   | 0.01   |
| Toshiba   | 2.5" HDD MK..59GSX     | 1      | 1       | 1450  | 1185  | 0.00   |
| Seagate   | Momentus 5400 FDE.2    | 1      | 1       | 446   | 494   | 0.00   |
| Seagate   | Pipeline HD 5900.1     | 1      | 1       | 469   | 609   | 0.00   |
| Hitachi   | Travelstar DK23XX/D... | 1      | 1       | 4     | 31    | 0.00   |
| Hitachi   | CinemaStar 5K1000      | 1      | 1       | 9     | 142   | 0.00   |
| Maxtor    | DiamondMax Plus 8      | 1      | 1       | 20    | 1133  | 0.00   |
| Toshiba   | 2.5" HDD MK..59GSM     | 1      | 1       | 8     | 558   | 0.00   |
| Toshiba   | 2.5" HDD MK..76GSX     | 1      | 1       | 2     | 1008  | 0.00   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| HP          | 6      | 18      | 2414  | 2     | 4.68   |
| Hitachi     | 99     | 271     | 1304  | 115   | 2.72   |
| CLOVER      | 1      | 1       | 928   | 0     | 2.54   |
| WDC         | 466    | 1326    | 1042  | 29    | 2.32   |
| Samsung     | 47     | 128     | 1258  | 167   | 2.31   |
| Lenovo      | 1      | 4       | 802   | 0     | 2.20   |
| HPE         | 4      | 19      | 706   | 1     | 1.90   |
| MaxDigital  | 1      | 1       | 681   | 0     | 1.87   |
| Maxtor      | 13     | 20      | 886   | 178   | 1.83   |
| HGST        | 41     | 198     | 745   | 111   | 1.74   |
| ExcelStor   | 2      | 4       | 1009  | 8     | 1.64   |
| Seagate     | 246    | 1101    | 836   | 139   | 1.63   |
| IBM         | 1      | 1       | 522   | 0     | 1.43   |
| Toshiba     | 90     | 326     | 554   | 60    | 1.24   |
| MediaMax    | 1      | 3       | 697   | 6     | 0.89   |
| Fujitsu     | 19     | 22      | 456   | 47    | 0.87   |
| Apple       | 7      | 12      | 317   | 5     | 0.63   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See full list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| OCZ       | VERTEX2            | 64 GB  | 1       | 2937  | 0     | 8.05   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 1       | 2739  | 0     | 7.51   |
| Intel     | SSDMCEAC120B3      | 120 GB | 1       | 2735  | 0     | 7.49   |
| Transcend | TS64GMSA340        | 64 GB  | 1       | 2696  | 0     | 7.39   |
| Kingston  | SVP180S2128G       | 128 GB | 1       | 2596  | 0     | 7.11   |
| G.Skill   | FM-25S3-120GBP3    | 120 GB | 1       | 2532  | 0     | 6.94   |
| Corsair   | Force 3 SSD        | 240 GB | 2       | 2472  | 0     | 6.77   |
| Intel     | SSDSC2BB240G4      | 240 GB | 1       | 2392  | 0     | 6.56   |
| Intel     | TK0080GDSAE        | 80 GB  | 1       | 2368  | 0     | 6.49   |
| OCZ       | VERTEX3 MI         | 240 GB | 1       | 2309  | 0     | 6.33   |
| Samsung   | MZ7GE480HMHP-00003 | 480 GB | 1       | 2235  | 0     | 6.12   |
| Micron    | P400m100-MTFDDA... | 100 GB | 1       | 2158  | 0     | 5.91   |
| Intel     | SSDSC2BB160G4      | 160 GB | 1       | 2147  | 0     | 5.88   |
| OCZ       | SOLID3             | 120 GB | 1       | 2144  | 0     | 5.87   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 1       | 2089  | 0     | 5.72   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 1       | 2014  | 0     | 5.52   |
| Corsair   | Force GT           | 240 GB | 1       | 1999  | 0     | 5.48   |
| Samsung   | MMCRE28G5MXP-0VB   | 128 GB | 1       | 1998  | 0     | 5.47   |
| HP        | VK0800GDJYA        | 800 GB | 1       | 1986  | 0     | 5.44   |
| HPE       | MK0400GCTZA        | 400 GB | 2       | 1980  | 0     | 5.43   |
| Intel     | SSDSC2BA200G4      | 200 GB | 1       | 1970  | 0     | 5.40   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 1       | 1964  | 0     | 5.38   |
| Intel     | SSDSC2BF120A5      | 120 GB | 1       | 1960  | 0     | 5.37   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 1       | 1923  | 0     | 5.27   |
| OCZ       | VERTEX PLUS        | 64 GB  | 1       | 1901  | 0     | 5.21   |
| ADATA     | SP310              | 32 GB  | 2       | 1889  | 0     | 5.18   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 1       | 1861  | 0     | 5.10   |
| Intel     | SSDSC2BB240G6      | 240 GB | 3       | 1848  | 0     | 5.06   |
| Samsung   | SSD PB22-JS3 TM    | 64 GB  | 1       | 1801  | 0     | 4.94   |
| OCZ       | AGILITY4           | 256 GB | 1       | 1775  | 0     | 4.87   |
| Samsung   | MZ7WD480HAGM-000D3 | 480 GB | 1       | 1752  | 0     | 4.80   |
| SanDisk   | SDSA5AK-008G-1006  | 8 GB   | 1       | 1749  | 0     | 4.79   |
| Toshiba   | TR150              | 120 GB | 1       | 1746  | 0     | 4.79   |
| Intel     | SSDSC2BB300G4      | 304 GB | 1       | 1746  | 0     | 4.78   |
| Intel     | SSDSC2CW180A3      | 180 GB | 1       | 1696  | 0     | 4.65   |
| Kingston  | SVP200S3120G       | 120 GB | 1       | 1677  | 0     | 4.60   |
| Toshiba   | THNSNX032GTNT M... | 32 GB  | 1       | 1665  | 0     | 4.56   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 1       | 1656  | 0     | 4.54   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 11      | 1647  | 0     | 4.51   |
| Samsung   | SSD 850 PRO        | 128 GB | 7       | 1615  | 0     | 4.43   |
| Intel     | SSDSA2CW120G3      | 120 GB | 4       | 1614  | 0     | 4.42   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 12      | 1613  | 0     | 4.42   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 2       | 1593  | 0     | 4.36   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 2       | 1581  | 0     | 4.33   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 2       | 1576  | 0     | 4.32   |
| ADATA     | SP920SS            | 128 GB | 1       | 1542  | 0     | 4.22   |
| OCZ       | AGILITY3           | 120 GB | 7       | 1577  | 173   | 4.22   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 2       | 1537  | 0     | 4.21   |
| Transcend | TS8GSSD500         | 8 GB   | 1       | 1520  | 0     | 4.17   |
| ADATA     | SP310              | 128 GB | 1       | 1488  | 0     | 4.08   |
| Samsung   | MZMTD128HAFV-000L1 | 128 GB | 1       | 1487  | 0     | 4.08   |
| Samsung   | MZ-5EA2000-0D3     | 200 GB | 4       | 1475  | 0     | 4.04   |
| Toshiba   | THNSNH512GBST      | 512 GB | 1       | 1460  | 0     | 4.00   |
| Samsung   | MZYTY128HDHP-000L2 | 128 GB | 1       | 1456  | 0     | 3.99   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 1       | 1449  | 0     | 3.97   |
| SanDisk   | PU1000064GBATSSD   | 64 GB  | 1       | 1449  | 0     | 3.97   |
| SanDisk   | SDSSDXP480G        | 480 GB | 2       | 1447  | 0     | 3.97   |
| Samsung   | SSD 840 EVO        | 120 GB | 19      | 1781  | 22    | 3.93   |
| Samsung   | SSD 830 Series     | 256 GB | 3       | 1435  | 0     | 3.93   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 9       | 1428  | 0     | 3.91   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 1       | 1425  | 0     | 3.91   |
| Micron    | M550_MTFDDAT256MAY | 256 GB | 1       | 1421  | 0     | 3.89   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 2       | 1416  | 0     | 3.88   |
| Samsung   | SSD PB22-JS3 FD... | 128 GB | 1       | 1414  | 0     | 3.88   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 1       | 1408  | 0     | 3.86   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 1       | 1400  | 0     | 3.84   |
| Intel     | SSDSC2CT180A4      | 180 GB | 3       | 1870  | 1     | 3.82   |
| Intel     | SSDSC2BA400G3      | 400 GB | 1       | 1388  | 0     | 3.80   |
| Samsung   | SSD PB22-JS3 2.5"  | 128 GB | 1       | 1365  | 0     | 3.74   |
| SanDisk   | SSD U100           | 8 GB   | 1       | 1365  | 0     | 3.74   |
| Innodisk  | Corp. DRPS-08GJ... | 8 GB   | 1       | 1364  | 0     | 3.74   |
| Plextor   | PX-512M5Pro        | 512 GB | 1       | 1361  | 0     | 3.73   |
| Intel     | SSDSC2BP240G4      | 240 GB | 2       | 1350  | 0     | 3.70   |
| AMD       | R3SL120G           | 120 GB | 2       | 1341  | 0     | 3.68   |
| Intel     | SSDMCEAC030B3      | 32 GB  | 5       | 1331  | 0     | 3.65   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 2       | 1298  | 0     | 3.56   |
| Kingston  | SVP200S37A60G      | 64 GB  | 5       | 1297  | 0     | 3.56   |
| Micro ... | G2 series          | 64 GB  | 1       | 1297  | 0     | 3.55   |
| SuperM... | SSD                | 128 GB | 1       | 1295  | 0     | 3.55   |
| Samsung   | MZ7LM240HCGR-0E003 | 240 GB | 2       | 1295  | 0     | 3.55   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 1       | 1285  | 0     | 3.52   |
| HPE       | MK000480GWCEV      | 480 GB | 2       | 1275  | 0     | 3.49   |
| HPE       | MK000960GWCFA      | 960 GB | 2       | 1275  | 0     | 3.49   |
| Corsair   | Force GS           | 128 GB | 2       | 1274  | 0     | 3.49   |
| SK hynix  | SC300 SATA         | 512 GB | 1       | 1266  | 0     | 3.47   |
| Seagate   | XF1230-1A0480      | 480 GB | 2       | 1266  | 0     | 3.47   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 2       | 1260  | 0     | 3.45   |
| Samsung   | MZNTY256HDHP-000L2 | 256 GB | 1       | 1258  | 0     | 3.45   |
| Intel     | SSDSC2CT180A3      | 180 GB | 4       | 1740  | 1     | 3.44   |
| Toshiba   | THNSFJ256GDNU      | 256 GB | 1       | 1250  | 0     | 3.43   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 4       | 1238  | 0     | 3.39   |
| Toshiba   | THNSNJ128GCSY      | 128 GB | 1       | 1236  | 0     | 3.39   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 1       | 1235  | 0     | 3.38   |
| OCZ       | AGILITY3           | 128 GB | 1       | 1233  | 0     | 3.38   |
| Kingston  | SH103S3240G        | 240 GB | 2       | 1224  | 0     | 3.36   |
| SanDisk   | Ultra II           | 960 GB | 2       | 1202  | 0     | 3.29   |
| Samsung   | SSD 830 Series     | 128 GB | 8       | 1197  | 0     | 3.28   |
| Samsung   | SSD 840 PRO Series | 128 GB | 15      | 1329  | 108   | 3.25   |
| Samsung   | SG9XCS1F50GMIBM... | 50 GB  | 1       | 1184  | 0     | 3.24   |
| Intel     | SSDSC2BB960G7R     | 960 GB | 6       | 1177  | 0     | 3.23   |
| SuperM... | SSD                | 16 GB  | 1       | 1176  | 0     | 3.22   |
| Dell      | SSDSCKJB120G7R     | 120 GB | 2       | 1173  | 0     | 3.22   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 3       | 1162  | 0     | 3.18   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 1154  | 0     | 3.16   |
| Intel     | SSDSC2BX400G4      | 400 GB | 1       | 1145  | 0     | 3.14   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 1       | 1131  | 0     | 3.10   |
| SanDisk   | SD6SF1M128G        | 128 GB | 1       | 1121  | 0     | 3.07   |
| Samsung   | MZMPC256HBGJ-000L1 | 256 GB | 1       | 1118  | 0     | 3.06   |
| Intel     | SSDSC2CW240A3      | 240 GB | 5       | 1117  | 0     | 3.06   |
| Kingston  | SM2280S3G2120G     | 120 GB | 1       | 1117  | 0     | 3.06   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 2       | 1117  | 0     | 3.06   |
| ADATA     | SP900              | 64 GB  | 3       | 1111  | 0     | 3.05   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 1105  | 0     | 3.03   |
| Intel     | SSDSC2BB080G6      | 80 GB  | 2       | 1101  | 0     | 3.02   |
| Samsung   | SSD 840 Series     | 120 GB | 14      | 1098  | 0     | 3.01   |
| ADATA     | SP600              | 32 GB  | 2       | 1097  | 0     | 3.01   |
| HP        | VK0480GECQP        | 480 GB | 1       | 1083  | 0     | 2.97   |
| OCZ       | VERTEX3            | 240 GB | 1       | 1081  | 0     | 2.96   |
| OCZ       | VERTEX3            | 64 GB  | 4       | 1591  | 8     | 2.96   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 1       | 1080  | 0     | 2.96   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 1       | 2157  | 1     | 2.96   |
| SanDisk   | SD7SF6S512G1122    | 512 GB | 1       | 1073  | 0     | 2.94   |
| Samsung   | SSD 840 EVO        | 500 GB | 6       | 1159  | 140   | 2.92   |
| Kingston  | SKC400S37512G      | 512 GB | 2       | 1059  | 0     | 2.90   |
| Apple     | SSD SD512E         | 500 GB | 1       | 1056  | 0     | 2.89   |
| Samsung   | SSD 750 EVO        | 250 GB | 8       | 1054  | 0     | 2.89   |
| Crucial   | FCCT128M4SSD1      | 128 GB | 2       | 1042  | 0     | 2.86   |
| Samsung   | SSD 850 EVO        | 120 GB | 13      | 1039  | 0     | 2.85   |
| Goodram   | SSD                | 240 GB | 3       | 1037  | 0     | 2.84   |
| BIWIN     | SSD                | 120 GB | 1       | 1033  | 0     | 2.83   |
| KingSpec  | NT-64              | 64 GB  | 1       | 1033  | 0     | 2.83   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 1       | 1012  | 0     | 2.77   |
| Intel     | SSDSA2CW160G3      | 160 GB | 3       | 1001  | 0     | 2.74   |
| ADATA     | SX930              | 240 GB | 1       | 1001  | 0     | 2.74   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 5       | 998   | 0     | 2.73   |
| Samsung   | SSD 840 Series     | 250 GB | 6       | 990   | 0     | 2.71   |
| Intel     | SSDMCEAW080A4      | 80 GB  | 1       | 981   | 0     | 2.69   |
| WDC       | WDBNCE5000PNC      | 500 GB | 3       | 981   | 0     | 2.69   |
| Crucial   | CT250MX200SSD1     | 250 GB | 5       | 1048  | 1     | 2.68   |
| Mushkin   | MKNSSDEC120GB      | 120 GB | 1       | 979   | 0     | 2.68   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 1       | 976   | 0     | 2.67   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 1       | 975   | 0     | 2.67   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 4       | 972   | 0     | 2.66   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 3       | 969   | 0     | 2.66   |
| OCZ       | AGILITY3           | 64 GB  | 4       | 969   | 0     | 2.66   |
| Seagate   | ST240HM000-1G5152  | 240 GB | 1       | 967   | 0     | 2.65   |
| SanDisk   | SD9SB8W256G1122    | 256 GB | 1       | 961   | 0     | 2.63   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 1       | 959   | 0     | 2.63   |
| SanDisk   | X600 2.5 7MM SATA  | 256 GB | 1       | 947   | 0     | 2.59   |
| Kingston  | SH103S3120G        | 120 GB | 5       | 940   | 0     | 2.58   |
| SanDisk   | SSD U100           | 16 GB  | 5       | 928   | 0     | 2.54   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 1       | 918   | 0     | 2.52   |
| OCZ       | VERTEX4            | 128 GB | 4       | 1127  | 1     | 2.48   |
| SanDisk   | SD8SBBU240G1122    | 240 GB | 1       | 891   | 0     | 2.44   |
| Seagate   | ST100FN0021        | 100 GB | 1       | 1781  | 1     | 2.44   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 1       | 888   | 0     | 2.44   |
| HPE       | MK000240GWEZF      | 240 GB | 2       | 882   | 0     | 2.42   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 4       | 881   | 0     | 2.41   |
| Samsung   | SSD 840 PRO Series | 256 GB | 13      | 1164  | 7     | 2.38   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 1       | 862   | 0     | 2.36   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 5       | 856   | 0     | 2.35   |
| Team      | L3 EVO SSD         | 120 GB | 1       | 854   | 0     | 2.34   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 2       | 848   | 0     | 2.33   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 4       | 848   | 0     | 2.32   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 7       | 844   | 0     | 2.31   |
| Corsair   | Force 3 SSD        | 180 GB | 1       | 2530  | 2     | 2.31   |
| OCZ       | VERTEX2            | 120 GB | 1       | 835   | 0     | 2.29   |
| Intel     | SSDSCKHB120G4      | 120 GB | 2       | 834   | 0     | 2.29   |
| PNY       | CS1311 240GB SSD   | 240 GB | 3       | 833   | 0     | 2.28   |
| Kingston  | SM2280S3120G       | 120 GB | 1       | 833   | 0     | 2.28   |
| Silico... | SP-mSATA-64G       | 64 GB  | 1       | 828   | 0     | 2.27   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 4       | 826   | 0     | 2.26   |
| Toshiba   | THNSNC128GBSJ      | 128 GB | 1       | 826   | 0     | 2.26   |
| Kingston  | SV300S37A60G       | 64 GB  | 10      | 1213  | 82    | 2.26   |
| Intel     | SSDSC2BB480G7      | 480 GB | 3       | 940   | 1     | 2.26   |
| Lite-On   | LAT-256M3S         | 256 GB | 1       | 820   | 0     | 2.25   |
| Kingston  | SUV400S37120G      | 120 GB | 6       | 820   | 0     | 2.25   |
| Kingston  | SMS200S360G        | 64 GB  | 9       | 1185  | 7     | 2.25   |
| Samsung   | SSD 850 EVO        | 250 GB | 80      | 817   | 0     | 2.24   |
| Intel     | SSDSC2BB120G4      | 120 GB | 10      | 939   | 1     | 2.24   |
| ADATA     | SP600              | 128 GB | 1       | 813   | 0     | 2.23   |
| Samsung   | SSD 830 Series     | 64 GB  | 2       | 812   | 0     | 2.23   |
| Apple     | SSD SM0512F        | 500 GB | 2       | 812   | 0     | 2.23   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 6       | 811   | 0     | 2.22   |
| Kingston  | SUV300S37A240G     | 240 GB | 1       | 807   | 0     | 2.21   |
| Plextor   | PH6-CE120-G        | 120 GB | 1       | 804   | 0     | 2.20   |
| Samsung   | SSD 850 PRO        | 512 GB | 16      | 803   | 0     | 2.20   |
| ADATA     | SSD S599           | 40 GB  | 1       | 802   | 0     | 2.20   |
| SK hynix  | SC311 SATA         | 128 GB | 1       | 802   | 0     | 2.20   |
| Advantech | SQF-SLMM2-8G-S8C   | 8 GB   | 1       | 801   | 0     | 2.20   |
| SanDisk   | X300 MSATA         | 256 GB | 1       | 800   | 0     | 2.19   |
| Kingston  | SV300S37A240G      | 240 GB | 7       | 798   | 0     | 2.19   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 2       | 798   | 0     | 2.19   |
| Plextor   | PX-64G5Le          | 64 GB  | 1       | 791   | 0     | 2.17   |
| Crucial   | CT960M500SSD1      | 960 GB | 2       | 787   | 0     | 2.16   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 3       | 787   | 0     | 2.16   |
| Corsair   | Force GT           | 120 GB | 2       | 1377  | 2     | 2.16   |
| Crucial   | CT240M500SSD3      | 240 GB | 3       | 783   | 0     | 2.15   |
| Samsung   | MZNLN128HCGR-000L1 | 128 GB | 1       | 781   | 0     | 2.14   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 4       | 778   | 0     | 2.13   |
| V-GeN     | V-GEN11SM18EG120GB | 120 GB | 1       | 777   | 0     | 2.13   |
| SanDisk   | SSD U110           | 128 GB | 1       | 776   | 0     | 2.13   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 2       | 1071  | 163   | 2.12   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 4       | 768   | 0     | 2.11   |
| Kingston  | SMS151S332GD1      | 32 GB  | 1       | 767   | 0     | 2.10   |
| SanDisk   | SDSSDHP128G        | 128 GB | 1       | 766   | 0     | 2.10   |
| Toshiba   | Q300               | 480 GB | 2       | 762   | 0     | 2.09   |
| China     | 240GB SSD          | 240 GB | 1       | 753   | 0     | 2.06   |
| Apple     | SSD TS256C         | 256 GB | 1       | 752   | 0     | 2.06   |
| Samsung   | SSD CM871 2.5 7mm  | 128 GB | 1       | 750   | 0     | 2.06   |
| SanDisk   | SSD U100           | 24 GB  | 2       | 745   | 0     | 2.04   |
| Samsung   | SSD 850 EVO        | 2 TB   | 1       | 742   | 0     | 2.03   |
| Phison    | SATA SSD           | 120 GB | 4       | 741   | 0     | 2.03   |
| Toshiba   | Q300               | 120 GB | 1       | 740   | 0     | 2.03   |
| Samsung   | SSD RBX Series ... | 64 GB  | 2       | 739   | 0     | 2.03   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 13      | 737   | 0     | 2.02   |
| Mushkin   | MKNSSDTR1TB-3DL    | 1 TB   | 1       | 734   | 0     | 2.01   |
| Samsung   | MZMPA016HMCD-000L1 | 16 GB  | 1       | 1467  | 1     | 2.01   |
| Samsung   | SSD 840 EVO        | 250 GB | 30      | 732   | 0     | 2.01   |
| Samsung   | SSD RBX Series ... | 128 GB | 1       | 1463  | 1     | 2.00   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 2       | 717   | 0     | 1.97   |
| Intel     | SSDSC2BW120A4      | 120 GB | 8       | 713   | 0     | 1.95   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 3       | 710   | 0     | 1.95   |
| Samsung   | MZNLN512HMJP-000L7 | 512 GB | 1       | 710   | 0     | 1.95   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 1       | 709   | 0     | 1.94   |
| SanDisk   | SD5SB2-128G-1006E  | 128 GB | 1       | 708   | 0     | 1.94   |
| Toshiba   | TL100              | 240 GB | 1       | 707   | 0     | 1.94   |
| Kingston  | SUV400S37240G      | 240 GB | 7       | 757   | 1     | 1.94   |
| Goodram   | SSD                | 120 GB | 5       | 700   | 0     | 1.92   |
| Corsair   | Force 3 SSD        | 64 GB  | 3       | 697   | 0     | 1.91   |
| Intel     | SSDSCKHW240A4      | 240 GB | 1       | 695   | 0     | 1.90   |
| Toshiba   | THNSNC128GMLJ      | 128 GB | 1       | 692   | 0     | 1.90   |
| Toshiba   | THNSNF256GMCS      | 256 GB | 1       | 690   | 0     | 1.89   |
| Kingston  | SHFS37A240G        | 240 GB | 3       | 689   | 0     | 1.89   |
| ADATA     | SP600              | 64 GB  | 2       | 683   | 0     | 1.87   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 8       | 681   | 0     | 1.87   |
| Samsung   | SSD 850 EVO        | 1 TB   | 11      | 1043  | 1     | 1.86   |
| SanDisk   | SD7SB7S-512G-1006  | 512 GB | 1       | 677   | 0     | 1.86   |
| Dogfish   | SSD 30G            | 32 GB  | 1       | 676   | 0     | 1.85   |
| Kingston  | SUV500120G         | 120 GB | 2       | 676   | 0     | 1.85   |
| Transcend | TS64GSSD340        | 64 GB  | 2       | 672   | 0     | 1.84   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 2       | 669   | 0     | 1.83   |
| Apple     | SSD TS128C         | 121 GB | 2       | 667   | 0     | 1.83   |
| Samsung   | SSD 850 EVO        | 500 GB | 37      | 690   | 1     | 1.82   |
| SanDisk   | SDSSDP128G         | 128 GB | 7       | 662   | 0     | 1.81   |
| Goodram   | SSDPR-CX400-128    | 128 GB | 2       | 659   | 0     | 1.81   |
| Lite-On   | LCH-128V2S-HP      | 128 GB | 1       | 659   | 0     | 1.81   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 2       | 658   | 0     | 1.80   |
| OWC       | Mercury Extreme... | 240 GB | 1       | 657   | 0     | 1.80   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 2       | 650   | 0     | 1.78   |
| Kingston  | SMSM150S324G2      | 24 GB  | 1       | 650   | 0     | 1.78   |
| Samsung   | SG9MSM6D024GPM00   | 22 GB  | 1       | 649   | 0     | 1.78   |
| OWC       | Mercury Electra... | 240 GB | 2       | 649   | 0     | 1.78   |
| Smartbuy  | SSD                | 240 GB | 1       | 647   | 0     | 1.77   |
| OCZ       | ARC100             | 240 GB | 3       | 646   | 0     | 1.77   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 2       | 646   | 0     | 1.77   |
| SanDisk   | SSD PLUS 120 GB    | 120 GB | 2       | 759   | 1     | 1.77   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 1       | 642   | 0     | 1.76   |
| Intel     | SSDSC2KW512G8      | 512 GB | 1       | 641   | 0     | 1.76   |
| OCZ       | VERTEX3            | 120 GB | 6       | 1115  | 28    | 1.75   |
| Transcend | TS128GMTS400S      | 128 GB | 1       | 637   | 0     | 1.75   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 1       | 635   | 0     | 1.74   |
| Samsung   | MZNLN512HMJP-000H1 | 512 GB | 1       | 633   | 0     | 1.74   |
| Corsair   | Force GS           | 180 GB | 2       | 631   | 0     | 1.73   |
| Mach X... | MXSSD2MSLD16G-V    | 16 GB  | 1       | 629   | 0     | 1.73   |
| Phison    | BP4 mSATA SSD      | 240 GB | 1       | 628   | 0     | 1.72   |
| Kingston  | SS200S330G         | 32 GB  | 3       | 624   | 0     | 1.71   |
| Samsung   | SSD 850 PRO        | 256 GB | 18      | 623   | 0     | 1.71   |
| Innodisk  | Corp. mSATA 3SE... | 2 GB   | 1       | 617   | 0     | 1.69   |
| SanDisk   | SDSSDP064G         | 64 GB  | 4       | 616   | 0     | 1.69   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 1       | 612   | 0     | 1.68   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 4       | 888   | 8     | 1.68   |
| Kingston  | SV300S37A120G      | 120 GB | 32      | 868   | 2     | 1.68   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 8       | 612   | 0     | 1.68   |
| ADATA     | SP900              | 128 GB | 4       | 611   | 0     | 1.68   |
| Transcend | TSG128MTS400ISI    | 128 GB | 1       | 609   | 0     | 1.67   |
| SanDisk   | SDSSDXP120G        | 120 GB | 1       | 608   | 0     | 1.67   |
| Goodram   | IRIDIUM PRO        | 120 GB | 1       | 599   | 0     | 1.64   |
| Team      | TEAML5Lite3D1T     | 1 TB   | 1       | 596   | 0     | 1.63   |
| Apacer    | AS510S             | 128 GB | 1       | 592   | 0     | 1.62   |
| Micron    | MTFDDAK120MBB-1... | 120 GB | 1       | 590   | 0     | 1.62   |
| SanDisk   | SDSA6GM-016G-1006  | 16 GB  | 1       | 589   | 0     | 1.62   |
| Kingston  | HyperX Fury 3D     | 240 GB | 1       | 588   | 0     | 1.61   |
| Kingston  | SMS200S330G        | 32 GB  | 8       | 927   | 2     | 1.61   |
| SK hynix  | SH920 mSATA        | 128 GB | 1       | 586   | 0     | 1.61   |
| Intel     | SSDSC2BB012T7      | 1.2 TB | 2       | 1169  | 1     | 1.60   |
| Kingston  | SKC300S37A240G     | 240 GB | 1       | 583   | 0     | 1.60   |
| Vaseky    | V800-32G           | 32 GB  | 1       | 582   | 0     | 1.60   |
| SPCC      | SSD                | 64 GB  | 4       | 574   | 0     | 1.57   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 4       | 570   | 0     | 1.56   |
| Kingston  | SUV400S37480G      | 480 GB | 1       | 566   | 0     | 1.55   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 8       | 2289  | 7     | 1.55   |
| Samsung   | MZNLN256HAJQ-000H1 | 256 GB | 1       | 558   | 0     | 1.53   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 4       | 553   | 0     | 1.52   |
| Samsung   | MZ7TE512HMHP-000L2 | 512 GB | 1       | 551   | 0     | 1.51   |
| Samsung   | MZ7TE128HMGR-000H1 | 128 GB | 1       | 550   | 0     | 1.51   |
| China     | SATA SSD           | 16 GB  | 38      | 549   | 0     | 1.51   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 2       | 548   | 0     | 1.50   |
| Crucial   | CT1050MX300SSD4    | 1 TB   | 2       | 1074  | 3     | 1.50   |
| Intel     | SSDSC2BB150G7      | 150 GB | 5       | 653   | 1     | 1.50   |
| Crucial   | CT256MX100SSD1     | 256 GB | 8       | 546   | 0     | 1.50   |
| Phison    | SATA SSD           | 16 GB  | 45      | 544   | 0     | 1.49   |
| Corsair   | Force LS SSD       | 64 GB  | 4       | 848   | 1     | 1.48   |
| Samsung   | SSD 750 EVO        | 120 GB | 3       | 540   | 0     | 1.48   |
| Kingston  | SHFS37A120G        | 120 GB | 8       | 735   | 1     | 1.48   |
| Seagate   | ST400FP0021        | 400 GB | 1       | 539   | 0     | 1.48   |
| KingFast  | SSD                | 16 GB  | 5       | 538   | 0     | 1.48   |
| Apacer    | AS220              | 64 GB  | 1       | 536   | 0     | 1.47   |
| Smartbuy  | SSD                | 120 GB | 1       | 532   | 0     | 1.46   |
| Intel     | SSDSC2BW240H6      | 240 GB | 4       | 526   | 0     | 1.44   |
| SanDisk   | SSD i110           | 32 GB  | 3       | 986   | 340   | 1.44   |
| Innodisk  | Corp. - mSATA 3IE3 | 64 GB  | 1       | 523   | 0     | 1.44   |
| Apple     | SSD SM256C         | 256 GB | 1       | 520   | 0     | 1.43   |
| Corsair   | CSSD-F60GB2        | 64 GB  | 1       | 516   | 0     | 1.42   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 5       | 510   | 0     | 1.40   |
| Advantech | SQF-SLMM2-8G-8SE   | 8 GB   | 3       | 509   | 0     | 1.40   |
| Phison    | SATA SSD           | 8 GB   | 1       | 508   | 0     | 1.39   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 1       | 508   | 0     | 1.39   |
| Toshiba   | A100               | 240 GB | 1       | 503   | 0     | 1.38   |
| Kingston  | SV300S37A480G      | 480 GB | 1       | 501   | 0     | 1.37   |
| Innodisk  | DEMSR- 16GB mSA... | 16 GB  | 2       | 501   | 0     | 1.37   |
| V-GeN     | V-GEN08AS19FS120IT | 120 GB | 1       | 500   | 0     | 1.37   |
| SanDisk   | Ultra II           | 480 GB | 5       | 497   | 0     | 1.36   |
| ADATA     | IM2S3134N-064GM    | 64 GB  | 7       | 492   | 0     | 1.35   |
| SanDisk   | SD8TB8U512G1001    | 512 GB | 2       | 489   | 0     | 1.34   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 7       | 1691  | 581   | 1.34   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 2       | 487   | 0     | 1.34   |
| Apacer    | 32GB SATA Flash... | 32 GB  | 6       | 756   | 171   | 1.33   |
| Plextor   | PX-128M7VC         | 128 GB | 1       | 483   | 0     | 1.32   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 1       | 483   | 0     | 1.32   |
| Samsung   | SSD 860 EVO        | 2 TB   | 3       | 480   | 0     | 1.32   |
| Corsair   | Force LE SSD       | 120 GB | 1       | 480   | 0     | 1.32   |
| Apacer    | 64GB SATA Flash... | 64 GB  | 7       | 536   | 29    | 1.31   |
| OCZ       | VERTEX2 3.5        | 120 GB | 1       | 472   | 0     | 1.30   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 6       | 472   | 0     | 1.29   |
| Samsung   | SSD 750 EVO        | 500 GB | 2       | 471   | 0     | 1.29   |
| KingSpec  | KSD-SA25.7-016MJ   | 16 GB  | 1       | 471   | 0     | 1.29   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 2       | 470   | 0     | 1.29   |
| SanDisk   | SDSSDA120G         | 120 GB | 21      | 477   | 35    | 1.29   |
| PNY       | CS900 120GB SSD    | 120 GB | 17      | 468   | 0     | 1.28   |
| Crucial   | CT128M550SSD4      | 128 GB | 1       | 466   | 0     | 1.28   |
| Intel     | SSDSC2BA400G4      | 400 GB | 1       | 465   | 0     | 1.28   |
| SanDisk   | X400 M.2 2280      | 256 GB | 2       | 465   | 0     | 1.28   |
| Delkin... | ME16TGPXQ-XN000-D  | 16 GB  | 1       | 916   | 1     | 1.26   |
| Intel     | SSDMCEAW120A4      | 120 GB | 4       | 456   | 0     | 1.25   |
| CWDISK    | SSD                | 32 GB  | 1       | 455   | 0     | 1.25   |
| SPCC      | SSD                | 120 GB | 8       | 452   | 0     | 1.24   |
| Toshiba   | THNSNH128GBST      | 128 GB | 1       | 450   | 0     | 1.23   |
| SanDisk   | SDSSDH3 1T02       | 1 TB   | 1       | 449   | 0     | 1.23   |
| SanDisk   | SDSSDHII120G       | 120 GB | 3       | 448   | 0     | 1.23   |
| Micron    | 5200_MTFDDAK1T9TDN | 1.9 TB | 2       | 446   | 0     | 1.22   |
| AEGO      | SSD                | 120 GB | 1       | 445   | 0     | 1.22   |
| Intel     | SSDSC2BF180A4H     | 180 GB | 4       | 444   | 0     | 1.22   |
| Hoodisk   | SSD                | 16 GB  | 12      | 441   | 0     | 1.21   |
| Samsung   | SSD PM830 FDE 2... | 256 GB | 1       | 440   | 0     | 1.21   |
| Intenso   | lntenso SSD Sat... | 120 GB | 1       | 438   | 0     | 1.20   |
| Phison    | SATA SSD           | 128 GB | 5       | 438   | 0     | 1.20   |
| MyDigi... | SB2                | 128 GB | 2       | 872   | 4     | 1.20   |
| ADATA     | SU750              | 1 TB   | 1       | 435   | 0     | 1.19   |
| Apacer    | 16GB SATA Flash... | 16 GB  | 9       | 513   | 3     | 1.19   |
| Plextor   | PX-AG256M6e        | 256 GB | 1       | 432   | 0     | 1.19   |
| SanDisk   | Ultra II           | 240 GB | 2       | 432   | 0     | 1.19   |
| Micron    | MTFDDAK256TBN-1... | 256 GB | 1       | 431   | 0     | 1.18   |
| Samsung   | MZNTE256HMHP-000L2 | 256 GB | 1       | 430   | 0     | 1.18   |
| Crucial   | CT480BX300SSD1     | 480 GB | 1       | 429   | 0     | 1.18   |
| Intel     | SSDSC2CT120A3      | 120 GB | 4       | 653   | 2     | 1.17   |
| Vaseky    | V800-60G           | 64 GB  | 1       | 426   | 0     | 1.17   |
| SK hynix  | SC300 M.2 2280     | 128 GB | 1       | 425   | 0     | 1.17   |
| SATADOM   | ML 3SE             | 64 GB  | 1       | 425   | 0     | 1.16   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 1       | 424   | 0     | 1.16   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 1       | 422   | 0     | 1.16   |
| China     | SATA SSD           | 128 GB | 4       | 421   | 0     | 1.15   |
| Samsung   | MZ7LH480HAHQ-00005 | 480 GB | 2       | 417   | 0     | 1.14   |
| Samsung   | MZMTE128HMGR-00007 | 128 GB | 2       | 416   | 0     | 1.14   |
| KST       | V300               | 119 GB | 1       | 416   | 0     | 1.14   |
| Intel     | SSDSC2BP480G4      | 480 GB | 2       | 415   | 0     | 1.14   |
| ADATA     | SSD S510           | 64 GB  | 1       | 414   | 0     | 1.14   |
| OCZ       | VERTEX2 3.5        | 240 GB | 1       | 413   | 0     | 1.13   |
| SanDisk   | SD6SB1M064G1022I   | 64 GB  | 5       | 412   | 0     | 1.13   |
| China     | SATA SSD           | 120 GB | 10      | 411   | 0     | 1.13   |
| Innodisk  | mSATA mini 3ME4    | 64 GB  | 1       | 411   | 0     | 1.13   |
| Patriot   | Pyro SSD           | 240 GB | 1       | 409   | 0     | 1.12   |
| Intel     | SSDSC2BW240A4      | 240 GB | 2       | 409   | 0     | 1.12   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 2       | 816   | 8     | 1.12   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 2       | 408   | 0     | 1.12   |
| Mushkin   | MKNSSDRE500GB      | 500 GB | 1       | 406   | 0     | 1.11   |
| SanDisk   | X400 M.2 2280      | 128 GB | 2       | 404   | 0     | 1.11   |
| Intel     | SSDSC2KW256G8      | 256 GB | 12      | 413   | 1     | 1.11   |
| SanDisk   | SDSSDA240G         | 240 GB | 17      | 452   | 5     | 1.10   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 1       | 400   | 0     | 1.10   |
| Advantech | SQF-S25M4-16G-S9C  | 16 GB  | 1       | 400   | 0     | 1.10   |
| Transcend | TS120GESD240C      | 120 GB | 1       | 397   | 0     | 1.09   |
| Intel     | SSDSC2BW120A3      | 120 GB | 2       | 984   | 508   | 1.08   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 6       | 415   | 3     | 1.08   |
| Plextor   | PX-256M5Pro        | 256 GB | 1       | 392   | 0     | 1.07   |
| TCSUNBOW  | X3                 | 480 GB | 1       | 391   | 0     | 1.07   |
| Samsung   | MZMTD256HAGM-000L1 | 256 GB | 1       | 391   | 0     | 1.07   |
| Kingston  | SMS100S264G        | 64 GB  | 1       | 389   | 0     | 1.07   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 2       | 388   | 0     | 1.06   |
| Innodisk  | DEMSR- 08GB mSA... | 8 GB   | 1       | 386   | 0     | 1.06   |
| Samsung   | SSD 840 EVO        | 1 TB   | 4       | 385   | 0     | 1.06   |
| KingSpec  | P3-120             | 120 GB | 1       | 385   | 0     | 1.06   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 1       | 385   | 0     | 1.06   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 4       | 384   | 0     | 1.05   |
| Samsung   | SSD 840 Series     | 500 GB | 2       | 649   | 1     | 1.05   |
| SPCC      | SSD                | 1 TB   | 19      | 384   | 0     | 1.05   |
| Hoodisk   | SSD                | 32 GB  | 32      | 383   | 0     | 1.05   |
| SanDisk   | SD9SB8W128G1122    | 128 GB | 1       | 381   | 0     | 1.05   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 6       | 392   | 1     | 1.04   |
| OCZ       | VECTOR150          | 120 GB | 1       | 758   | 1     | 1.04   |
| Patriot   | Burst              | 960 GB | 2       | 378   | 0     | 1.04   |
| KingDian  | S280               | 240 GB | 1       | 378   | 0     | 1.04   |
| PNY       | CS1311 120GB SSD   | 120 GB | 2       | 375   | 0     | 1.03   |
| SanDisk   | SDSSDHII240G       | 240 GB | 1       | 374   | 0     | 1.03   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 4       | 374   | 0     | 1.03   |
| OCZ       | TRION150           | 480 GB | 1       | 373   | 0     | 1.02   |
| Transcend | TS128GSSD370S      | 128 GB | 3       | 372   | 0     | 1.02   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 1       | 369   | 0     | 1.01   |
| Netac     | SSD                | 64 GB  | 1       | 366   | 0     | 1.00   |
| AVEXIR    | E100 SERIES -      | 120 GB | 1       | 365   | 0     | 1.00   |
| SanDisk   | SDSSDH3500G        | 500 GB | 1       | 365   | 0     | 1.00   |
| Apacer    | APSDM050GM1AN-T... | 54 GB  | 1       | 364   | 0     | 1.00   |
| SanDisk   | SDSSDHII960G       | 960 GB | 2       | 364   | 0     | 1.00   |
| Crucial   | CT240M500SSD1      | 240 GB | 5       | 546   | 328   | 0.99   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 2       | 361   | 0     | 0.99   |
| Transcend | TS128GMTS400       | 128 GB | 2       | 360   | 0     | 0.99   |
| Zheino    | CHN-mSATAM3-256    | 256 GB | 2       | 360   | 0     | 0.99   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 3       | 358   | 0     | 0.98   |
| Toshiba   | TR200              | 480 GB | 1       | 358   | 0     | 0.98   |
| SanDisk   | SD8TN8U256G1001    | 256 GB | 2       | 356   | 0     | 0.98   |
| Samsung   | MZ7KM960HAHP-0Z005 | 960 GB | 1       | 356   | 0     | 0.98   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 2       | 356   | 0     | 0.98   |
| China     | SATA2 32GB SSD     | 32 GB  | 1       | 354   | 0     | 0.97   |
| ADATA     | SU655              | 120 GB | 1       | 353   | 0     | 0.97   |
| Kingston  | SVP100S2512G       | 512 GB | 1       | 353   | 0     | 0.97   |
| Kingston  | RBUSNS8180S3128GI  | 128 GB | 1       | 351   | 0     | 0.96   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 2       | 351   | 0     | 0.96   |
| Transcend | TS32GSSD340K       | 32 GB  | 2       | 351   | 0     | 0.96   |
| SanDisk   | SDSSDP256G         | 256 GB | 2       | 349   | 0     | 0.96   |
| SK hynix  | SC311 SATA         | 256 GB | 3       | 349   | 0     | 0.96   |
| Kingston  | SV200S3128G        | 128 GB | 1       | 1746  | 4     | 0.96   |
| SanDisk   | SSD U110           | 16 GB  | 9       | 348   | 0     | 0.96   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 1       | 347   | 0     | 0.95   |
| Samsung   | SSD 860 PRO        | 1 TB   | 5       | 345   | 0     | 0.95   |
| DST       | DST8128-MSATA-1... | 128 GB | 1       | 345   | 0     | 0.95   |
| Protectli | 16GB mSATA         | 16 GB  | 1       | 341   | 0     | 0.94   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 3       | 341   | 0     | 0.93   |
| HP        | SSD S600           | 120 GB | 1       | 339   | 0     | 0.93   |
| Kingston  | SUV500MS120G       | 120 GB | 51      | 337   | 0     | 0.92   |
| Samsung   | MZ7LF192HCGS-000L1 | 192 GB | 1       | 335   | 0     | 0.92   |
| SanDisk   | SD8SN8U128G1001    | 128 GB | 1       | 335   | 0     | 0.92   |
| Lite-On   | IT LCS-256L9S      | 256 GB | 1       | 334   | 0     | 0.92   |
| SanDisk   | SD6SP1M256G1102    | 256 GB | 1       | 333   | 0     | 0.91   |
| Mushkin   | MKNSSDAT120GB-V    | 120 GB | 1       | 332   | 0     | 0.91   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 1       | 332   | 0     | 0.91   |
| SanDisk   | SD6SB1M-032G-1006  | 32 GB  | 1       | 331   | 0     | 0.91   |
| OCZ       | AGILITY4           | 128 GB | 2       | 370   | 1     | 0.90   |
| Vaseky    | V800-120G          | 120 GB | 1       | 325   | 0     | 0.89   |
| OCZ       | TRION150           | 240 GB | 2       | 325   | 0     | 0.89   |
| Intel     | SSDSC2KB480G8R     | 480 GB | 1       | 325   | 0     | 0.89   |
| TCSUNBOW  | M1                 | 32 GB  | 4       | 322   | 0     | 0.88   |
| Kingston  | SUV500M8120G       | 120 GB | 1       | 320   | 0     | 0.88   |
| SanDisk   | SDSSDH32000G       | 2 TB   | 1       | 319   | 0     | 0.87   |
| Samsung   | SSD 840 PRO Series | 512 GB | 1       | 319   | 0     | 0.87   |
| Faspeed   | H5-240G            | 240 GB | 1       | 318   | 0     | 0.87   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 1       | 316   | 0     | 0.87   |
| Mushkin   | MKNSSDRE250GB-LT   | 250 GB | 1       | 312   | 0     | 0.86   |
| Toshiba   | THNSNX032GTNT      | 32 GB  | 1       | 312   | 0     | 0.86   |
| OCZ       | AGILITY3           | 240 GB | 1       | 1553  | 4     | 0.85   |
| China     | SATA SSD           | 32 GB  | 11      | 437   | 11    | 0.85   |
| Kingston  | SUV300S37A120G     | 120 GB | 1       | 309   | 0     | 0.85   |
| Crucial   | CT250MX200SSD3     | 250 GB | 1       | 308   | 0     | 0.85   |
| Hoodisk   | SSD                | 512 GB | 3       | 308   | 0     | 0.84   |
| Samsung   | MZYLF128HCHP-000L2 | 128 GB | 1       | 307   | 0     | 0.84   |
| Hyundai   | 120GB SSD          | 120 GB | 1       | 306   | 0     | 0.84   |
| Toshiba   | KSG60ZMV256G M.... | 256 GB | 3       | 306   | 0     | 0.84   |
| Intenso   | SSD Sata III       | 120 GB | 6       | 305   | 0     | 0.84   |
| Intel     | SSDSC2BW180A4      | 180 GB | 5       | 304   | 0     | 0.83   |
| Corsair   | CMFSSD-256D1       | 256 GB | 1       | 303   | 0     | 0.83   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 1       | 303   | 0     | 0.83   |
| KingDian  | S400               | 120 GB | 1       | 303   | 0     | 0.83   |
| Transcend | 3E128-TS2-550B01   | 100 GB | 4       | 404   | 257   | 0.83   |
| Phison    | SATA SSD           | 32 GB  | 7       | 301   | 0     | 0.83   |
| Crucial   | CT500MX200SSD1     | 500 GB | 5       | 300   | 0     | 0.82   |
| Samsung   | SSD 860 EVO        | 500 GB | 52      | 299   | 0     | 0.82   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 3       | 296   | 0     | 0.81   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 12      | 296   | 0     | 0.81   |
| Intel     | SSDSC2CT240A3      | 240 GB | 1       | 2370  | 7     | 0.81   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 3       | 1438  | 29    | 0.81   |
| SanDisk   | SSD U110           | 24 GB  | 1       | 295   | 0     | 0.81   |
| Samsung   | SSD 860 EVO        | 250 GB | 45      | 295   | 0     | 0.81   |
| WDC       | WDS200T2B0A        | 2 TB   | 1       | 588   | 1     | 0.81   |
| Samsung   | MZ7LN128HAHQ-000L2 | 128 GB | 1       | 293   | 0     | 0.80   |
| Crucial   | CT525MX300SSD1     | 528 GB | 12      | 550   | 2     | 0.80   |
| Samsung   | MZHPV256HDGL-00000 | 256 GB | 1       | 292   | 0     | 0.80   |
| Corsair   | Force LS SSD       | 120 GB | 2       | 290   | 0     | 0.80   |
| Toshiba   | TR200              | 240 GB | 5       | 287   | 0     | 0.79   |
| Samsung   | MZ7TD128HAFV-00000 | 128 GB | 1       | 286   | 0     | 0.79   |
| Intel     | SSDMCEAC060B3      | 64 GB  | 1       | 572   | 1     | 0.78   |
| KIOXIA... | SATA SSD           | 240 GB | 1       | 286   | 0     | 0.78   |
| China     | G7-240G PLUS       | 240 GB | 1       | 285   | 0     | 0.78   |
| Crucial   | CT250MX500SSD4     | 250 GB | 2       | 285   | 0     | 0.78   |
| WDC       | WDS500G2B0A        | 500 GB | 5       | 283   | 0     | 0.78   |
| SanDisk   | SSD U100           | 128 GB | 1       | 282   | 0     | 0.77   |
| SMART     | SSD XceedValue2... | 32 GB  | 1       | 280   | 0     | 0.77   |
| HP        | SSD S700 Pro       | 512 GB | 2       | 280   | 0     | 0.77   |
| SanDisk   | SD9SN8W128G1002    | 128 GB | 1       | 278   | 0     | 0.76   |
| SK hynix  | SC401 SATA         | 512 GB | 1       | 278   | 0     | 0.76   |
| Hoodisk   | SSD                | 128 GB | 33      | 277   | 0     | 0.76   |
| Protectli | 32GB mSATA         | 32 GB  | 3       | 276   | 0     | 0.76   |
| Apacer    | AS350              | 120 GB | 1       | 274   | 0     | 0.75   |
| China     | NGFF 2242 32GB SSD | 32 GB  | 1       | 273   | 0     | 0.75   |
| Transcend | TS120GMTS420S      | 120 GB | 10      | 272   | 0     | 0.75   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 2       | 272   | 0     | 0.75   |
| Kingston  | SKC400S37256G      | 256 GB | 1       | 271   | 0     | 0.74   |
| Transcend | TS64GMTS400S       | 64 GB  | 2       | 271   | 0     | 0.74   |
| SanDisk   | SD6SB2M512G1022I   | 512 GB | 1       | 536   | 1     | 0.74   |
| SK hynix  | HFS128G32MND-2200A | 128 GB | 1       | 798   | 2     | 0.73   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 1       | 264   | 0     | 0.72   |
| SanDisk   | X400 M.2 2280      | 512 GB | 2       | 263   | 0     | 0.72   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 1       | 263   | 0     | 0.72   |
| WDC       | WDBNCE2500PNC      | 250 GB | 3       | 263   | 0     | 0.72   |
| Intel     | SSDSC2CW120A3      | 120 GB | 5       | 1708  | 815   | 0.71   |
| SK hynix  | HFS256G39TND-N210A | 256 GB | 3       | 257   | 0     | 0.71   |
| Intel     | SSDSA2CW300G3      | 304 GB | 1       | 256   | 0     | 0.70   |
| Hoodisk   | SSD                | 64 GB  | 38      | 255   | 0     | 0.70   |
| Intel     | SSDSC2KB240G8      | 240 GB | 14      | 254   | 0     | 0.70   |
| Gigabyte  | GP-GSTFS31256GTND  | 256 GB | 2       | 252   | 0     | 0.69   |
| OWC       | Mercury Electra... | 1 TB   | 5       | 252   | 0     | 0.69   |
| XrayDisk  | SSD                | 64 GB  | 1       | 251   | 0     | 0.69   |
| Samsung   | MZMTE128HMGR-00000 | 128 GB | 1       | 251   | 0     | 0.69   |
| Apple     | SSD SM1024G        | 1 TB   | 1       | 251   | 0     | 0.69   |
| China     | M10C               | 256 GB | 2       | 249   | 0     | 0.68   |
| Kston     | SSD                | 32 GB  | 2       | 248   | 0     | 0.68   |
| Crucial   | CT275MX300SSD4     | 275 GB | 3       | 319   | 59    | 0.68   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 1       | 245   | 0     | 0.67   |
| SanDisk   | SD5SE2256G1002E    | 256 GB | 3       | 290   | 1     | 0.67   |
| Intenso   | JAJMS600M128G      | 128 GB | 1       | 245   | 0     | 0.67   |
| Apple     | SSD SM0512G        | 500 GB | 3       | 244   | 0     | 0.67   |
| Indilinx  | IND-S3MP-256G      | 256 GB | 1       | 243   | 0     | 0.67   |
| Plextor   | PX-128M5S          | 128 GB | 1       | 1216  | 4     | 0.67   |
| Samsung   | MZNTE256HMHP-000H1 | 256 GB | 1       | 242   | 0     | 0.66   |
| Seagate   | ZA240NM10001       | 240 GB | 1       | 240   | 0     | 0.66   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 1       | 239   | 0     | 0.66   |
| China     | SATA SSD           | 64 GB  | 2       | 239   | 0     | 0.66   |
| Patriot   | Burst              | 240 GB | 7       | 238   | 0     | 0.65   |
| Crucial   | CT120M500SSD1      | 120 GB | 5       | 735   | 4     | 0.65   |
| Ramaxel   | RTNTE256PCA8EADL   | 256 GB | 1       | 235   | 0     | 0.65   |
| PNY       | CS900 250GB SSD    | 250 GB | 2       | 235   | 0     | 0.65   |
| Samsung   | MZ7LN256HMJP-000L7 | 256 GB | 1       | 234   | 0     | 0.64   |
| ASENNO    | ASN8               | 240 GB | 1       | 231   | 0     | 0.63   |
| Crucial   | CT250MX500SSD1     | 250 GB | 51      | 231   | 0     | 0.63   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 1       | 231   | 0     | 0.63   |
| Plextor   | PX-256M8VG         | 256 GB | 1       | 230   | 0     | 0.63   |
| Kingston  | SMSM150S3128G      | 128 GB | 1       | 229   | 0     | 0.63   |
| Intenso   | SSD SATAIII        | 120 GB | 4       | 229   | 1     | 0.63   |
| Crucial   | CT500MX500SSD4     | 500 GB | 6       | 228   | 0     | 0.63   |
| KingSpec  | MT-64              | 64 GB  | 2       | 225   | 0     | 0.62   |
| Plextor   | PX-128M5Pro        | 128 GB | 1       | 224   | 0     | 0.61   |
| SanDisk   | SD8SBAT256G1122    | 256 GB | 1       | 223   | 0     | 0.61   |
| Samsung   | MZHPV512HDGL-000L1 | 512 GB | 1       | 222   | 0     | 0.61   |
| Corsair   | CSSD-V64GB2        | 64 GB  | 1       | 221   | 0     | 0.61   |
| PNY       | CS900 240GB SSD    | 240 GB | 13      | 220   | 0     | 0.60   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 12      | 231   | 1     | 0.60   |
| Samsung   | MZ7TY128HDHP-00000 | 128 GB | 1       | 218   | 0     | 0.60   |
| Intel     | SSDSA2M160G2GN     | 160 GB | 1       | 3720  | 16    | 0.60   |
| Transcend | TS16GMTS400        | 16 GB  | 1       | 217   | 0     | 0.60   |
| Kingston  | SHSS37A240G        | 240 GB | 2       | 217   | 0     | 0.60   |
| Intel     | SSDSA2M120G2GC     | 120 GB | 1       | 1086  | 4     | 0.60   |
| Samsung   | SSD 860 EVO        | 1 TB   | 31      | 217   | 1     | 0.59   |
| ADATA     | SU650              | 480 GB | 2       | 216   | 0     | 0.59   |
| SPCC      | SSD                | 240 GB | 2       | 214   | 0     | 0.59   |
| SanDisk   | SSD PLUS           | 1 TB   | 5       | 214   | 0     | 0.59   |
| WDC       | WDS500G2B0B-00YS70 | 500 GB | 7       | 214   | 0     | 0.59   |
| Transcend | TS64GSSD370S       | 64 GB  | 3       | 214   | 0     | 0.59   |
| Samsung   | Portable SSD T5    | 500 GB | 3       | 213   | 0     | 0.58   |
| SanDisk   | SSD PLUS           | 120 GB | 22      | 212   | 0     | 0.58   |
| Transcend | TS512GSSD370       | 512 GB | 2       | 212   | 0     | 0.58   |
| Kingston  | SMS200S3120G       | 120 GB | 10      | 641   | 17    | 0.58   |
| Lite-On   | IT LCS-128L9S-HP   | 128 GB | 2       | 211   | 0     | 0.58   |
| Corsair   | Force 3 SSD        | 120 GB | 4       | 813   | 254   | 0.58   |
| Kingston  | SA400S37240G       | 240 GB | 78      | 212   | 1     | 0.58   |
| SanDisk   | SD5SG2128G1052E    | 128 GB | 2       | 222   | 1     | 0.58   |
| SanDisk   | SDSSDH3512G        | 512 GB | 2       | 209   | 0     | 0.57   |
| WDC       | WDS100T1R0B-68A4Z0 | 1 TB   | 1       | 209   | 0     | 0.57   |
| HP        | SSD S700 Pro       | 256 GB | 1       | 207   | 0     | 0.57   |
| Apple     | SSD SD0128F        | 121 GB | 2       | 370   | 1     | 0.57   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 1       | 207   | 0     | 0.57   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 6       | 288   | 1     | 0.57   |
| OCZ       | VERTEX4            | 64 GB  | 1       | 206   | 0     | 0.57   |
| Samsung   | SSD 650            | 120 GB | 2       | 205   | 0     | 0.56   |
| Kingston  | SUV500240G         | 240 GB | 3       | 205   | 0     | 0.56   |
| SanDisk   | SD8TN8U512G1001    | 512 GB | 1       | 204   | 0     | 0.56   |
| Seagate   | FireCuda 120 SS... | 1 TB   | 2       | 204   | 0     | 0.56   |
| Samsung   | SSD 860 PRO        | 512 GB | 9       | 204   | 0     | 0.56   |
| Seagate   | BarraCuda 120 S... | 500 GB | 1       | 204   | 0     | 0.56   |
| Intel     | SSDSC2BW180A3H     | 180 GB | 1       | 203   | 0     | 0.56   |
| Corsair   | Neutron SSD        | 128 GB | 1       | 202   | 0     | 0.55   |
| WDC       | WDS100T1R0A-68A4W0 | 1 TB   | 1       | 202   | 0     | 0.55   |
| Intel     | SSDSC2BF240A4H     | 240 GB | 1       | 201   | 0     | 0.55   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 1       | 200   | 0     | 0.55   |
| Kingston  | SA400S37120G       | 120 GB | 64      | 199   | 0     | 0.55   |
| HP        | SSD S700           | 1 TB   | 1       | 198   | 0     | 0.54   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 1       | 196   | 0     | 0.54   |
| Kingston  | SUV500M8240G       | 240 GB | 3       | 196   | 0     | 0.54   |
| Intel     | SSDSC2BW480A4      | 480 GB | 1       | 976   | 4     | 0.53   |
| Intel     | SSDMCEAW240A4      | 240 GB | 1       | 973   | 4     | 0.53   |
| Transcend | TS64GSSD370        | 64 GB  | 6       | 193   | 0     | 0.53   |
| Hoodisk   | SSD                | 256 GB | 9       | 192   | 0     | 0.53   |
| Crucial   | CT120BX500SSD1     | 120 GB | 34      | 190   | 0     | 0.52   |
| KingFast  | SSD                | 128 GB | 1       | 189   | 0     | 0.52   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 7       | 189   | 0     | 0.52   |
| Pioneer   | APS-SL3N-128       | 128 GB | 1       | 189   | 0     | 0.52   |
| SanDisk   | SSD PLUS           | 240 GB | 17      | 235   | 3     | 0.52   |
| Innodisk  | Corp. DRPS-16GJ... | 16 GB  | 1       | 187   | 0     | 0.51   |
| Lite-On   | LCH-128V2S-11 2... | 128 GB | 1       | 186   | 0     | 0.51   |
| MyDigi... | SC2 M2 SSD         | 120 GB | 1       | 186   | 0     | 0.51   |
| Toshiba   | Q300               | 240 GB | 2       | 186   | 0     | 0.51   |
| Micron    | C400-MTFDDAT064MAM | 64 GB  | 2       | 184   | 0     | 0.51   |
| OCZ       | VERTEX3            | 128 GB | 1       | 184   | 0     | 0.50   |
| Goodram   | SSDPR-CL100-120-G2 | 120 GB | 2       | 183   | 0     | 0.50   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 2       | 183   | 0     | 0.50   |
| Patriot   | Burst              | 480 GB | 1       | 183   | 0     | 0.50   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 19      | 217   | 1     | 0.50   |
| Intel     | SSDSC2CT240A4      | 240 GB | 1       | 182   | 0     | 0.50   |
| China     | SSD 128G           | 128 GB | 1       | 181   | 0     | 0.50   |
| Kingston  | SM2280S3G2240G     | 240 GB | 1       | 181   | 0     | 0.50   |
| Samsung   | MZ7LH1T9HMLT0D3    | 1.9 TB | 2       | 180   | 0     | 0.50   |
| China     | SSD                | 64 GB  | 5       | 179   | 0     | 0.49   |
| Intel     | SSDSA2SH064G1GC    | 64 GB  | 1       | 179   | 0     | 0.49   |
| China     | DHMSR64GD81BC1QC   | 54 GB  | 2       | 177   | 0     | 0.49   |
| KingDian  | S280-240GB         | 240 GB | 1       | 177   | 0     | 0.49   |
| Smartbuy  | SSD                | 64 GB  | 2       | 176   | 0     | 0.48   |
| Kingston  | SA400S37960G       | 960 GB | 3       | 175   | 0     | 0.48   |
| Goodram   | IRP_SSDPR_S25B_480 | 480 GB | 1       | 174   | 0     | 0.48   |
| SK hynix  | SC308 SATA         | 256 GB | 3       | 222   | 2     | 0.48   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 2       | 172   | 0     | 0.47   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 1       | 172   | 0     | 0.47   |
| Patriot   | FLARE              | 64 GB  | 1       | 172   | 0     | 0.47   |
| Samsung   | MZMPC256HBGJ-00000 | 256 GB | 1       | 171   | 0     | 0.47   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 15      | 170   | 0     | 0.47   |
| SanDisk   | SDSSDH3 500G       | 500 GB | 3       | 170   | 0     | 0.47   |
| Samsung   | SSD 860 QVO        | 1 TB   | 12      | 169   | 0     | 0.46   |
| Kingston  | SMS200S3240G       | 240 GB | 1       | 168   | 0     | 0.46   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 1       | 166   | 0     | 0.46   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 3       | 198   | 74    | 0.45   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 2       | 164   | 0     | 0.45   |
| SanDisk   | SDSSDH3 512G       | 512 GB | 3       | 163   | 0     | 0.45   |
| China     | SATA3 64GB SSD     | 64 GB  | 2       | 162   | 0     | 0.45   |
| Samsung   | SSD 860 PRO        | 256 GB | 14      | 162   | 0     | 0.45   |
| Kingston  | SNV425S2128GB      | 128 GB | 1       | 1457  | 8     | 0.44   |
| Samsung   | MZNLN256HMHQ-000H1 | 256 GB | 1       | 161   | 0     | 0.44   |
| EMTEC     | X150               | 240 GB | 1       | 161   | 0     | 0.44   |
| Samsung   | SSD 860 QVO        | 2 TB   | 2       | 161   | 0     | 0.44   |
| Vaseky    | 128GV800           | 128 GB | 1       | 161   | 0     | 0.44   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 30      | 192   | 1     | 0.44   |
| Kingston  | SQ500S37240G       | 240 GB | 1       | 159   | 0     | 0.44   |
| Samsung   | SSD PM871b M.2 ... | 256 GB | 1       | 158   | 0     | 0.43   |
| OCZ       | VERTEX4            | 256 GB | 1       | 158   | 0     | 0.43   |
| SanDisk   | SD6SB1M064G        | 64 GB  | 1       | 157   | 0     | 0.43   |
| Transcend | TS240GMTS420S      | 240 GB | 6       | 157   | 0     | 0.43   |
| Lite-On   | CV3-CE128-HP       | 128 GB | 1       | 157   | 0     | 0.43   |
| China     | 40GB SATA Flash... | 40 GB  | 1       | 156   | 0     | 0.43   |
| ATP       | SATA III mSATA     | 120 GB | 4       | 156   | 0     | 0.43   |
| Kingston  | SUV500MS240G       | 240 GB | 29      | 156   | 0     | 0.43   |
| Lite-On   | LCH-128V2S         | 128 GB | 3       | 156   | 0     | 0.43   |
| Plextor   | PX-64M5M           | 64 GB  | 1       | 154   | 0     | 0.42   |
| Kingston  | SA400S37480G       | 480 GB | 24      | 158   | 1     | 0.42   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 1       | 153   | 0     | 0.42   |
| Samsung   | MMCQE28GFMUP-MVA   | 128 GB | 1       | 153   | 0     | 0.42   |
| SanDisk   | SSD i110           | 16 GB  | 1       | 152   | 0     | 0.42   |
| PNY       | CS1311 480GB SSD   | 480 GB | 1       | 152   | 0     | 0.42   |
| WDC       | WDS500G1R0B-68A4Z0 | 500 GB | 2       | 148   | 0     | 0.41   |
| Protectli | 960GB mSATA        | 960 GB | 2       | 147   | 0     | 0.40   |
| Transcend | TS256GSSD230S      | 256 GB | 1       | 147   | 0     | 0.40   |
| Samsung   | MZNLN256HCHP-000H1 | 256 GB | 1       | 146   | 0     | 0.40   |
| ADATA     | SU650              | 240 GB | 7       | 145   | 0     | 0.40   |
| Transcend | TS128GMSA230S      | 128 GB | 27      | 145   | 0     | 0.40   |
| SPCC      | SPCCSolidStateDisk | 256 GB | 3       | 144   | 0     | 0.40   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 5       | 144   | 0     | 0.40   |
| Lite-On   | CV8-8E256-11 SATA  | 256 GB | 1       | 143   | 0     | 0.39   |
| SPCC      | SSD                | 512 GB | 7       | 143   | 0     | 0.39   |
| KingSpec  | MT-128             | 128 GB | 4       | 139   | 0     | 0.38   |
| ADATA     | SU630              | 240 GB | 11      | 163   | 2     | 0.38   |
| Kingston  | RBUSNS8180DS3128GH | 128 GB | 2       | 139   | 0     | 0.38   |
| Patriot   | Burst              | 120 GB | 8       | 139   | 0     | 0.38   |
| Team      | TEAML5Lite3D120G   | 120 GB | 1       | 139   | 0     | 0.38   |
| Intenso   | SSD Sata III       | 250 GB | 2       | 138   | 0     | 0.38   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 2       | 137   | 0     | 0.38   |
| China     | SATA SSD           | 256 GB | 2       | 136   | 0     | 0.37   |
| Patriot   | Burst Elite        | 120 GB | 1       | 136   | 0     | 0.37   |
| China     | SATA3 120GB SSD    | 120 GB | 1       | 136   | 0     | 0.37   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 2       | 270   | 1     | 0.37   |
| Samsung   | SSD 860 QVO        | 4 TB   | 2       | 135   | 0     | 0.37   |
| Plextor   | PX-256M5M          | 256 GB | 1       | 135   | 0     | 0.37   |
| Intel     | SSDSC2KW128G8      | 128 GB | 3       | 134   | 0     | 0.37   |
| Samsung   | MZNTE128HMGR-000SO | 128 GB | 2       | 287   | 3     | 0.37   |
| Kston     | SSD                | 128 GB | 8       | 163   | 1     | 0.37   |
| KingFast  | SSD                | 120 GB | 18      | 131   | 51    | 0.36   |
| Samsung   | MZHPV256HDGL-000L1 | 256 GB | 1       | 131   | 0     | 0.36   |
| Micron    | MTFDDAK512TDL-1... | 512 GB | 1       | 131   | 0     | 0.36   |
| Intel     | SSDSC2BF240A5L     | 240 GB | 1       | 130   | 0     | 0.36   |
| Lite-On   | CV8-8E256          | 256 GB | 1       | 130   | 0     | 0.36   |
| ADATA     | SU650              | 120 GB | 17      | 242   | 78    | 0.35   |
| Samsung   | MZNLN256HMHQ-000H7 | 256 GB | 1       | 126   | 0     | 0.35   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 20      | 149   | 3     | 0.35   |
| Crucial   | CT275MX300SSD1     | 275 GB | 8       | 606   | 395   | 0.34   |
| Apacer    | AS450              | 240 GB | 1       | 123   | 0     | 0.34   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 1       | 123   | 0     | 0.34   |
| Lite-On   | LCS-128M6S-HP      | 128 GB | 1       | 123   | 0     | 0.34   |
| HPE       | MK000480GWUGF      | 480 GB | 1       | 369   | 2     | 0.34   |
| China     | SH00M120GB         | 120 GB | 2       | 122   | 0     | 0.34   |
| SanDisk   | SD7SN3Q128G1002    | 128 GB | 2       | 120   | 0     | 0.33   |
| SK hynix  | HFS128G32TNF-N3A0A | 128 GB | 2       | 119   | 0     | 0.33   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 1       | 119   | 0     | 0.33   |
| Kingston  | SQ500S37120G       | 120 GB | 2       | 118   | 0     | 0.33   |
| Apacer    | AS340              | 240 GB | 1       | 118   | 0     | 0.32   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 1       | 118   | 0     | 0.32   |
| ADATA     | SU810NS38 SATA ... | 256 GB | 1       | 117   | 0     | 0.32   |
| SK hynix  | SC311 SATA         | 512 GB | 2       | 117   | 0     | 0.32   |
| PNY       | CS900 500GB SSD    | 500 GB | 3       | 117   | 0     | 0.32   |
| SanDisk   | SSD i100           | 24 GB  | 1       | 117   | 0     | 0.32   |
| Verbatim  | Vi500 S3 480GB SSD | 480 GB | 1       | 115   | 0     | 0.32   |
| SanDisk   | SSD PLUS           | 480 GB | 6       | 148   | 1     | 0.32   |
| Toshiba   | THNSNC064GBSJ      | 64 GB  | 1       | 115   | 0     | 0.32   |
| China     | SATA SSD           | 240 GB | 4       | 115   | 0     | 0.32   |
| SanDisk   | SD9SN8W512G        | 512 GB | 1       | 114   | 0     | 0.31   |
| SPCC      | SSD                | 256 GB | 11      | 114   | 0     | 0.31   |
| ADATA     | SU700              | 240 GB | 1       | 114   | 0     | 0.31   |
| LDLC      | SSD                | 120 GB | 1       | 113   | 0     | 0.31   |
| Apple     | SSD TS128E         | 121 GB | 1       | 113   | 0     | 0.31   |
| ADATA     | SU800              | 256 GB | 5       | 112   | 0     | 0.31   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 4       | 796   | 11    | 0.31   |
| Crucial   | CT120BX300SSD1     | 120 GB | 3       | 112   | 0     | 0.31   |
| Crucial   | CT960BX500SSD1     | 960 GB | 2       | 112   | 0     | 0.31   |
| Apacer    | AS330              | 240 GB | 1       | 1006  | 8     | 0.31   |
| Mushkin   | MKNSSDRE1TB        | 1 TB   | 2       | 108   | 0     | 0.30   |
| Intel     | SSDMAEMC040G2      | 40 GB  | 1       | 217   | 1     | 0.30   |
| AMD       | R5SL240G           | 240 GB | 3       | 150   | 7     | 0.30   |
| China     | OSSD256GBTSS2      | 256 GB | 1       | 107   | 0     | 0.30   |
| Lite-On   | LCS-128L9S-11 2... | 128 GB | 2       | 107   | 0     | 0.29   |
| Dogfish   | SSD                | 512 GB | 4       | 107   | 0     | 0.29   |
| Transcend | TS32GSSD370S       | 32 GB  | 9       | 106   | 0     | 0.29   |
| Advantech | SQF-S25M8-128G-ABT | 128 GB | 1       | 106   | 0     | 0.29   |
| XUNZHE    | MSATA              | 128 GB | 1       | 106   | 0     | 0.29   |
| China     | BR                 | 64 GB  | 1       | 106   | 0     | 0.29   |
| Intel     | SSDSC2KG480G8R     | 480 GB | 2       | 105   | 0     | 0.29   |
| Phison    | SATA SSD           | 1 TB   | 1       | 105   | 0     | 0.29   |
| Lite-On   | LSS-24L6G          | 24 GB  | 1       | 105   | 0     | 0.29   |
| ADATA     | SU800              | 128 GB | 5       | 104   | 0     | 0.29   |
| SK hynix  | SHGS31-500GS-2     | 500 GB | 2       | 104   | 0     | 0.29   |
| China     | CF120GB            | 120 GB | 1       | 104   | 0     | 0.29   |
| Intenso   | SATA III SSD       | 480 GB | 1       | 102   | 0     | 0.28   |
| Crucial   | CT240BX500SSD1     | 240 GB | 35      | 102   | 0     | 0.28   |
| Intel     | SSDSA2M160G2HP     | 160 GB | 1       | 513   | 4     | 0.28   |
| FORESEE   | 32GB SSD           | 32 GB  | 4       | 102   | 0     | 0.28   |
| SPCC      | SSD                | 128 GB | 19      | 109   | 1     | 0.28   |
| Team      | T253X2512G         | 512 GB | 1       | 101   | 0     | 0.28   |
| Samsung   | MZNLN512HAJQ-00007 | 512 GB | 1       | 101   | 0     | 0.28   |
| ZTC       | SM201-064G         | 64 GB  | 2       | 593   | 13    | 0.28   |
| Crucial   | CT128M550SSD3      | 128 GB | 1       | 1705  | 16    | 0.27   |
| Apacer    | AS350              | 128 GB | 4       | 100   | 0     | 0.27   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 12      | 99    | 0     | 0.27   |
| EMTEC     | X250               | 512 GB | 1       | 98    | 0     | 0.27   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 8       | 98    | 0     | 0.27   |
| China     | 256GB QLC SATA SSD | 256 GB | 1       | 97    | 0     | 0.27   |
| Samsung   | MZNTY256HDHP-000H1 | 256 GB | 1       | 97    | 0     | 0.27   |
| Crucial   | CT500MX500SSD1     | 500 GB | 36      | 105   | 1     | 0.27   |
| China     | SATA SSD           | 20 GB  | 1       | 96    | 0     | 0.26   |
| BlueRay   | Ultra M8V          | 256 GB | 1       | 95    | 0     | 0.26   |
| Phison    | SATA SSD           | 64 GB  | 3       | 95    | 0     | 0.26   |
| BIWIN     | SSD                | 256 GB | 3       | 94    | 0     | 0.26   |
| Apacer    | 128GB SATA Flas... | 128 GB | 2       | 94    | 0     | 0.26   |
| Intel     | SSDSCKGF180A4L     | 180 GB | 2       | 94    | 0     | 0.26   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 3       | 94    | 0     | 0.26   |
| Intel     | SSDSC2BF180A5L     | 180 GB | 1       | 188   | 1     | 0.26   |
| Samsung   | MZMTE128HMGR-000MV | 128 GB | 1       | 94    | 0     | 0.26   |
| Lite-On   | L8H-256V2G         | 256 GB | 1       | 93    | 0     | 0.26   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 5       | 92    | 0     | 0.25   |
| Intel     | SSDSC2KG240G8      | 240 GB | 7       | 91    | 0     | 0.25   |
| Apple     | SSD SM0128G        | 121 GB | 2       | 91    | 0     | 0.25   |
| Ramsta    | SSD S300 Pro       | 256 GB | 1       | 91    | 0     | 0.25   |
| Apple     | SSD SM128E         | 121 GB | 1       | 89    | 0     | 0.25   |
| SanDisk   | SD8SBAT032G1122    | 32 GB  | 1       | 88    | 0     | 0.24   |
| Samsung   | MZMPC128HBFU-000L1 | 128 GB | 1       | 88    | 0     | 0.24   |
| Transcend | TS32GMSA370        | 32 GB  | 11      | 88    | 0     | 0.24   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 1       | 88    | 0     | 0.24   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 1       | 87    | 0     | 0.24   |
| SanDisk   | SSD G5 BICS4       | 1 TB   | 5       | 87    | 0     | 0.24   |
| SuperM... | SSD                | 64 GB  | 2       | 87    | 0     | 0.24   |
| China     | PATA SSD           | 8 GB   | 1       | 87    | 0     | 0.24   |
| Transcend | TS64GSSD420K       | 64 GB  | 1       | 86    | 0     | 0.24   |
| KingFast  | SSD                | 32 GB  | 1       | 85    | 0     | 0.24   |
| ADATA     | IM2S3144-030GK     | 32 GB  | 1       | 85    | 0     | 0.23   |
| Lite-On   | LMT-256L9M-11 M... | 256 GB | 1       | 84    | 0     | 0.23   |
| ADATA     | SU800              | 1 TB   | 1       | 83    | 0     | 0.23   |
| Faspeed   | K5M-32G            | 32 GB  | 4       | 82    | 0     | 0.23   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 1       | 82    | 0     | 0.23   |
| UDinfo    | M2S                | 120 GB | 3       | 82    | 0     | 0.23   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 1       | 81    | 0     | 0.22   |
| Samsung   | MZMPA024HMCD-000L1 | 24 GB  | 1       | 81    | 0     | 0.22   |
| Intel     | SSDSA2M080G2GN     | 80 GB  | 1       | 1136  | 13    | 0.22   |
| Intel     | SSDSA2BW160G3H     | 160 GB | 2       | 346   | 23    | 0.22   |
| Samsung   | MZNLN256HAJQ-000L7 | 256 GB | 2       | 79    | 0     | 0.22   |
| Kingston  | SA400M8240G        | 240 GB | 9       | 79    | 0     | 0.22   |
| Apacer    | APM050GMFAN-4MTM1  | 54 GB  | 1       | 78    | 0     | 0.21   |
| Intel     | SSDSC2KI128G8      | 100 GB | 2       | 77    | 0     | 0.21   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 1       | 76    | 0     | 0.21   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 2       | 75    | 0     | 0.21   |
| Intel     | SSDSC2BW120H6      | 120 GB | 4       | 176   | 267   | 0.21   |
| Kingston  | SMSM151S3128GD     | 128 GB | 1       | 598   | 7     | 0.21   |
| Goodram   | SSDPR-CX400-128-G2 | 128 GB | 1       | 73    | 0     | 0.20   |
| Mushkin   | MKNSSDTR240GB      | 240 GB | 1       | 73    | 0     | 0.20   |
| Innodisk  | Corp. - mSATA 3... | 64 GB  | 1       | 72    | 0     | 0.20   |
| Protectli | 120GB mSATA        | 120 GB | 15      | 72    | 0     | 0.20   |
| Indilinx  | InM2246S3-128G     | 128 GB | 1       | 71    | 0     | 0.20   |
| ADATA     | SU800NS38          | 256 GB | 2       | 71    | 0     | 0.19   |
| Micron    | M500_MTFDDAK960MAV | 960 GB | 4       | 1695  | 270   | 0.19   |
| Kingston  | SM2280S3240G       | 240 GB | 1       | 70    | 0     | 0.19   |
| KingSpec  | NT-128             | 128 GB | 2       | 70    | 0     | 0.19   |
| Dogfish   | SSD                | 480 GB | 1       | 210   | 2     | 0.19   |
| China     | XJH-128GB          | 128 GB | 4       | 69    | 0     | 0.19   |
| Team      | L5 LITE SSD        | 240 GB | 1       | 69    | 0     | 0.19   |
| Samsung   | SSD 860 EVO        | 4 TB   | 1       | 68    | 0     | 0.19   |
| Transcend | TS64GMSA230S       | 64 GB  | 16      | 68    | 0     | 0.19   |
| China     | SSD                | 128 GB | 5       | 68    | 0     | 0.19   |
| KingFast  | SSD                | 256 GB | 2       | 67    | 0     | 0.19   |
| Transcend | TS32GHSD370        | 32 GB  | 1       | 67    | 0     | 0.19   |
| Innodisk  | DEM24-32GM41BC1... | 32 GB  | 1       | 67    | 0     | 0.19   |
| Micron    | MTFDBAK128MAG-1G1  | 128 GB | 1       | 67    | 0     | 0.19   |
| Intel     | SSDSCKGF256A5 SATA | 256 GB | 1       | 67    | 0     | 0.19   |
| Drevo     | X1 SSD             | 64 GB  | 1       | 66    | 0     | 0.18   |
| Samsung   | MZMPC032HBCD-000H1 | 32 GB  | 1       | 66    | 0     | 0.18   |
| Drevo     | X1 pro 64G         | 64 GB  | 2       | 66    | 0     | 0.18   |
| OWC       | Mercury EXTREME... | 960 GB | 2       | 65    | 0     | 0.18   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 3       | 64    | 0     | 0.18   |
| Plextor   | PX-256M5S          | 256 GB | 2       | 64    | 0     | 0.18   |
| Intel     | SSDMAEXC024G3H     | 24 GB  | 1       | 63    | 0     | 0.17   |
| China     | mSATA-64GB SSD     | 64 GB  | 1       | 63    | 0     | 0.17   |
| Plextor   | PX-128M5M          | 128 GB | 3       | 61    | 0     | 0.17   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 8       | 61    | 0     | 0.17   |
| Apple     | SSD SM256E         | 256 GB | 4       | 261   | 31    | 0.17   |
| Intel     | SSDSCKJF240A5H REF | 240 GB | 1       | 60    | 0     | 0.17   |
| SanDisk   | SD7SN3Q512G1002    | 512 GB | 1       | 60    | 0     | 0.17   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 34      | 59    | 0     | 0.16   |
| Lite-On   | LSS-32L6G-HP       | 32 GB  | 1       | 59    | 0     | 0.16   |
| Samsung   | MZMTE1T0HMJH-00000 | 1 TB   | 1       | 59    | 0     | 0.16   |
| FORESEE   | 128GB SSD          | 128 GB | 28      | 59    | 0     | 0.16   |
| SanDisk   | SD6SF1M032G1022    | 32 GB  | 1       | 59    | 0     | 0.16   |
| Transcend | TS32GSSD370        | 32 GB  | 7       | 59    | 0     | 0.16   |
| Team      | T253X2001T         | 1 TB   | 1       | 58    | 0     | 0.16   |
| Hikvision | HKVSN HS-SSD-S2... | 512 GB | 1       | 58    | 0     | 0.16   |
| Intel     | SSDSC2MH120A2      | 120 GB | 2       | 57    | 0     | 0.16   |
| SanDisk   | SSD U100           | 32 GB  | 1       | 57    | 0     | 0.16   |
| Transcend | TS64GMTS400SD      | 64 GB  | 3       | 57    | 0     | 0.16   |
| Transcend | TS256GSSD320       | 256 GB | 2       | 170   | 3     | 0.16   |
| Goodram   | SSDPR-CX400-512-G2 | 512 GB | 1       | 56    | 0     | 0.15   |
| Micron    | 5210_MTFDDAK7T6QDE | 7.6 TB | 4       | 55    | 0     | 0.15   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 1       | 55    | 0     | 0.15   |
| Dogfish   | SSD                | 256 GB | 9       | 55    | 0     | 0.15   |
| SanDisk   | WD easystore       | 240 GB | 3       | 54    | 0     | 0.15   |
| Dogfish   | SSD                | 128 GB | 10      | 74    | 1     | 0.15   |
| SK hynix  | SHGS31-250GS-2     | 250 GB | 2       | 54    | 0     | 0.15   |
| China     | SSD                | 120 GB | 5       | 84    | 1     | 0.15   |
| China     | SATA3 480GB SSD    | 480 GB | 1       | 162   | 2     | 0.15   |
| Apacer    | 8GB SATA Flash ... | 8 GB   | 2       | 846   | 29    | 0.15   |
| Transcend | TS256GMTS800       | 256 GB | 1       | 53    | 0     | 0.15   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 1       | 53    | 0     | 0.15   |
| Transcend | TS256GMSA452T      | 256 GB | 2       | 53    | 0     | 0.15   |
| Lite-On   | LGT-128M6G         | 128 GB | 1       | 52    | 0     | 0.14   |
| SATADOM   | SL 3IE3 V2         | 64 GB  | 6       | 52    | 0     | 0.14   |
| Plextor   | PX-128M6S          | 128 GB | 2       | 50    | 0     | 0.14   |
| SanDisk   | SD9SN8W128G1102    | 128 GB | 2       | 50    | 0     | 0.14   |
| Transcend | TS64GMSA370        | 64 GB  | 16      | 50    | 0     | 0.14   |
| Lenovo    | SSD SL700 120G     | 120 GB | 1       | 50    | 0     | 0.14   |
| Lite-On   | L8H-256V2G-11 M... | 256 GB | 1       | 50    | 0     | 0.14   |
| OCZ       | VERTEX2            | 55 GB  | 1       | 50    | 0     | 0.14   |
| KingDian  | S280               | 120 GB | 1       | 49    | 0     | 0.14   |
| Dogfish   | SSD                | 64 GB  | 4       | 49    | 0     | 0.13   |
| SanDisk   | SD8TB8U-256G-1006  | 256 GB | 1       | 294   | 5     | 0.13   |
| ADATA     | SU630              | 480 GB | 1       | 48    | 0     | 0.13   |
| Transcend | TS128GSSD420K      | 128 GB | 1       | 48    | 0     | 0.13   |
| KingSpec  | MT-256             | 256 GB | 1       | 47    | 0     | 0.13   |
| Samsung   | SSD 870 QVO        | 8 TB   | 1       | 47    | 0     | 0.13   |
| Intenso   | SSD                | 128 GB | 8       | 47    | 0     | 0.13   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 3       | 46    | 0     | 0.13   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 2       | 46    | 0     | 0.13   |
| Intenso   | IONN SSD           | 256 GB | 2       | 45    | 0     | 0.13   |
| Toshiba   | THNSNJ256GCSY      | 256 GB | 1       | 45    | 0     | 0.12   |
| Transcend | TS128GMTS550T      | 128 GB | 1       | 44    | 0     | 0.12   |
| Intel     | SSDSA2BW160G3      | 160 GB | 1       | 44    | 0     | 0.12   |
| Micron    | MTFDDAT064MAM-1J2  | 64 GB  | 2       | 44    | 0     | 0.12   |
| China     | TYPEC 120GB PSSD   | 120 GB | 1       | 44    | 0     | 0.12   |
| SanDisk   | SD8SN8U-128G-1006  | 128 GB | 1       | 43    | 0     | 0.12   |
| SanDisk   | SSD i100           | 32 GB  | 3       | 477   | 4     | 0.12   |
| ADATA     | SU800              | 512 GB | 3       | 43    | 0     | 0.12   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 5       | 43    | 0     | 0.12   |
| minisf... | SSD                | 256 GB | 7       | 42    | 0     | 0.12   |
| China     | QST8-512           | 512 GB | 1       | 42    | 0     | 0.12   |
| China     | SSD 64G            | 64 GB  | 1       | 41    | 0     | 0.11   |
| SanDisk   | SD8SBAT128G1122    | 128 GB | 4       | 41    | 0     | 0.11   |
| Crucial   | CT480BX500SSD1     | 480 GB | 8       | 41    | 0     | 0.11   |
| Kingston  | SA400S37-240GB     | 240 GB | 1       | 41    | 0     | 0.11   |
| Samsung   | MZYLN256HCHP-000L2 | 256 GB | 1       | 41    | 0     | 0.11   |
| SanDisk   | SDSSDHP256G        | 256 GB | 1       | 41    | 0     | 0.11   |
| Zheino    | CHN mSATAM1 064    | 64 GB  | 1       | 41    | 0     | 0.11   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 2       | 40    | 0     | 0.11   |
| SanDisk   | pSSD               | 64 GB  | 5       | 40    | 0     | 0.11   |
| KingDian  | S200               | 64 GB  | 4       | 44    | 253   | 0.11   |
| Dogfish   | SSD                | 120 GB | 1       | 121   | 2     | 0.11   |
| ADATA     | ASU800SS-128GT     | 128 GB | 2       | 39    | 0     | 0.11   |
| Intel     | SSDSC2KW256G8L     | 256 GB | 1       | 39    | 0     | 0.11   |
| HPE       | MK000480GWXFF      | 480 GB | 2       | 39    | 0     | 0.11   |
| Kingston  | SUV500MS480G       | 480 GB | 7       | 38    | 0     | 0.11   |
| WDC       | WDS120G1G0B-00RC30 | 120 GB | 1       | 37    | 0     | 0.10   |
| Samsung   | MZ7LN256HCHP-000F0 | 256 GB | 1       | 37    | 0     | 0.10   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 1       | 37    | 0     | 0.10   |
| Goodram   | SSDPR-CL100-120-G3 | 120 GB | 6       | 37    | 0     | 0.10   |
| Kingston  | SUV400S37 120G     | 120 GB | 1       | 37    | 0     | 0.10   |
| Samsung   | MZ7LM240HMHQ-00005 | 240 GB | 1       | 36    | 0     | 0.10   |
| Samsung   | MZYTE256HMHP-000L2 | 256 GB | 1       | 36    | 0     | 0.10   |
| Intel     | SSDSC2KG480G8      | 480 GB | 7       | 36    | 0     | 0.10   |
| Micron    | 1100 SATA          | 512 GB | 1       | 36    | 0     | 0.10   |
| Samsung   | SSD 870 EVO        | 1 TB   | 9       | 58    | 1     | 0.10   |
| ADATA     | SU750              | 256 GB | 1       | 36    | 0     | 0.10   |
| KingSpec  | P3-256             | 256 GB | 1       | 35    | 0     | 0.10   |
| Fujitsu   | F500S 120G         | 120 GB | 1       | 35    | 0     | 0.10   |
| Phison    | SATA SSD           | 240 GB | 1       | 35    | 0     | 0.10   |
| Intenso   | SATA3 240GB SSD    | 240 GB | 1       | 35    | 0     | 0.10   |
| BIWIN     | SSD                | 128 GB | 13      | 106   | 20    | 0.10   |
| Transcend | TS128GMTS430S      | 128 GB | 4       | 34    | 0     | 0.10   |
| SanDisk   | SDSA6PM-064G-1006  | 64 GB  | 1       | 33    | 0     | 0.09   |
| Samsung   | SSD 870 QVO        | 1 TB   | 6       | 33    | 0     | 0.09   |
| MidasF... | SSD                | 256 GB | 1       | 32    | 0     | 0.09   |
| OCZ       | VERTEX-TURBO       | 32 GB  | 2       | 298   | 56    | 0.09   |
| FORESEE   | 64GB SSD           | 64 GB  | 12      | 31    | 0     | 0.09   |
| China     | KR 32G             | 32 GB  | 1       | 31    | 0     | 0.09   |
| Kingston  | HyperX Fury 3D ... | 480 GB | 2       | 31    | 0     | 0.09   |
| China     | NGFF 2242 512GB... | 512 GB | 1       | 31    | 0     | 0.09   |
| Goodram   | SSDPR-CX400-256-G2 | 256 GB | 3       | 30    | 0     | 0.08   |
| KingSpec  | NT-256             | 256 GB | 4       | 30    | 0     | 0.08   |
| Toshiba   | TL100              | 120 GB | 1       | 30    | 0     | 0.08   |
| Kston     | SSD                | 64 GB  | 6       | 29    | 0     | 0.08   |
| Transcend | TS256GMSA370       | 256 GB | 1       | 29    | 0     | 0.08   |
| KingDian  | S280               | 480 GB | 1       | 29    | 0     | 0.08   |
| China     | R580               | 64 GB  | 1       | 28    | 0     | 0.08   |
| SanDisk   | SD9TN8W256G1001    | 256 GB | 1       | 28    | 0     | 0.08   |
| Samsung   | MZNLN256HMHQ-000L7 | 256 GB | 1       | 27    | 0     | 0.08   |
| Apacer    | AS350              | 256 GB | 3       | 27    | 0     | 0.08   |
| Micron    | MTFDDAK256MAM-1K12 | 256 GB | 2       | 53    | 505   | 0.07   |
| Plextor   | PX-128G7Ne         | 128 GB | 1       | 189   | 6     | 0.07   |
| Transcend | TS32GMTS600        | 32 GB  | 2       | 26    | 0     | 0.07   |
| Lexar     | 256GB SSD          | 256 GB | 4       | 26    | 0     | 0.07   |
| Zheino    | CHN mSATA01M 060   | 64 GB  | 1       | 26    | 0     | 0.07   |
| Micron    | M550_MTFDDAK064MAY | 64 GB  | 1       | 26    | 0     | 0.07   |
| Apacer    | AS340              | 120 GB | 1       | 25    | 0     | 0.07   |
| Transcend | TS128GSSD370       | 128 GB | 1       | 25    | 0     | 0.07   |
| Transcend | TS256GMSA230S      | 256 GB | 14      | 24    | 0     | 0.07   |
| WDC       | PC SA530 SDASB8... | 256 GB | 1       | 24    | 0     | 0.07   |
| Protectli | 240GB mSATA        | 240 GB | 5       | 23    | 0     | 0.06   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 1       | 46    | 1     | 0.06   |
| Transcend | TS256GMTS952T2     | 256 GB | 11      | 22    | 0     | 0.06   |
| Kingston  | SKC600256G         | 256 GB | 2       | 22    | 0     | 0.06   |
| China     | CS2246-M512        | 506 GB | 1       | 22    | 0     | 0.06   |
| ATP       | SATA III M.2 2242  | 64 GB  | 1       | 22    | 0     | 0.06   |
| Samsung   | SSD 870 QVO        | 2 TB   | 6       | 22    | 0     | 0.06   |
| BR        | SSD 32G            | 32 GB  | 1       | 22    | 0     | 0.06   |
| Crucial   | CT512M550SSD1      | 512 GB | 1       | 379   | 16    | 0.06   |
| China     | BK-32GB MSATA SSD  | 32 GB  | 1       | 22    | 0     | 0.06   |
| Transcend | TS512GMSA370       | 512 GB | 1       | 21    | 0     | 0.06   |
| Transcend | TS128GMSA370       | 128 GB | 10      | 21    | 0     | 0.06   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 1       | 21    | 0     | 0.06   |
| Intenso   | SSD Sata III       | 256 GB | 3       | 21    | 0     | 0.06   |
| SanDisk   | SSD i100           | 64 GB  | 1       | 21    | 0     | 0.06   |
| Crucial   | CT128MX100SSD1     | 128 GB | 2       | 350   | 16    | 0.06   |
| Dogfish   | SSD                | 500 GB | 1       | 20    | 0     | 0.06   |
| Intel     | SSDSC2KF256H6L     | 256 GB | 1       | 61    | 2     | 0.06   |
| Transcend | TS512GMTS430S      | 512 GB | 1       | 20    | 0     | 0.06   |
| Netac     | S535N8-256GYN      | 256 GB | 1       | 20    | 0     | 0.06   |
| ORICO     | PH100-128G         | 128 GB | 1       | 19    | 0     | 0.05   |
| Samsung   | SSD PM871b M.2 ... | 128 GB | 1       | 19    | 0     | 0.05   |
| ADATA     | ASU800SS-256GT-2   | 256 GB | 1       | 19    | 0     | 0.05   |
| China     | Kston128GB         | 128 GB | 1       | 19    | 0     | 0.05   |
| SanPin    | mSATA-64GB         | 64 GB  | 1       | 19    | 0     | 0.05   |
| Lite-On   | CV3-CE128-11 SATA  | 128 GB | 1       | 19    | 0     | 0.05   |
| Samsung   | SSD 850 PRO        | 1 TB   | 2       | 19    | 0     | 0.05   |
| Zheino    | CHN HFmSATA01M 128 | 128 GB | 1       | 18    | 0     | 0.05   |
| MicroD... | 512G SSD           | 512 GB | 1       | 18    | 0     | 0.05   |
| SPCC      | SSD                | 55 GB  | 1       | 18    | 0     | 0.05   |
| ADATA     | SU655              | 240 GB | 1       | 18    | 0     | 0.05   |
| SanDisk   | SSD P4             | 16 GB  | 2       | 86    | 4     | 0.05   |
| Crucial   | CT250MX200SSD4     | 250 GB | 1       | 17    | 0     | 0.05   |
| Apacer    | 256GB SATA Flas... | 256 GB | 1       | 17    | 0     | 0.05   |
| Lite-On   | PH4-CE120          | 120 GB | 1       | 17    | 0     | 0.05   |
| Lite-On   | LMS-32L6M-HP       | 32 GB  | 1       | 16    | 0     | 0.05   |
| Apple     | A45ACXBA9TA        | 512 GB | 1       | 16    | 0     | 0.04   |
| SanDisk   | SD8SBAT064G1122    | 64 GB  | 1       | 15    | 0     | 0.04   |
| SETHRISE  | SSD 480G           | 480 GB | 1       | 14    | 0     | 0.04   |
| Apacer    | AS681              | 240 GB | 1       | 14    | 0     | 0.04   |
| Transcend | TS256GMTS400       | 256 GB | 1       | 14    | 0     | 0.04   |
| Samsung   | SSD 870 EVO        | 250 GB | 17      | 14    | 0     | 0.04   |
| SanDisk   | SD8SBAT-256G-1006  | 256 GB | 1       | 14    | 0     | 0.04   |
| Crucial   | CT525MX300SSD4     | 528 GB | 1       | 70    | 4     | 0.04   |
| China     | SH00M240GB         | 240 GB | 1       | 13    | 0     | 0.04   |
| Intel     | SSDSC2BF180A5H REF | 180 GB | 1       | 13    | 0     | 0.04   |
| Transcend | TS128GMTS800       | 128 GB | 1       | 13    | 0     | 0.04   |
| Intenso   | SSD Sata III       | 128 GB | 3       | 13    | 17    | 0.04   |
| Kingston  | HyperX Fury 3D     | 120 GB | 1       | 13    | 0     | 0.04   |
| Intel     | SSDSC2BF256A5 SATA | 256 GB | 1       | 360   | 26    | 0.04   |
| ADATA     | SP610              | 128 GB | 1       | 39    | 2     | 0.04   |
| Lite-On   | LMH-128V2M-11 M... | 128 GB | 1       | 13    | 0     | 0.04   |
| Corsair   | Voyager GTX        | 256 GB | 1       | 13    | 0     | 0.04   |
| PNY       | SSD2SC240G5LC70... | 240 GB | 1       | 13    | 0     | 0.04   |
| SanDisk   | SD8SBAT256G1002    | 256 GB | 2       | 12    | 0     | 0.04   |
| Lite-On   | CS1-SP32-11 M.2... | 32 GB  | 1       | 12    | 0     | 0.03   |
| Hikvision | HS-SSD-C100 120G   | 120 GB | 1       | 12    | 0     | 0.03   |
| Lite-On   | LCH-256V2S         | 256 GB | 2       | 12    | 0     | 0.03   |
| KingFast  | SSD                | 512 GB | 2       | 12    | 0     | 0.03   |
| NTC       | SSD                | 120 GB | 1       | 12    | 0     | 0.03   |
| Qunion    | P20A 64G           | 64 GB  | 1       | 12    | 0     | 0.03   |
| KingSpec  | NT-32              | 32 GB  | 1       | 12    | 0     | 0.03   |
| Netac     | SSD                | 240 GB | 1       | 11    | 0     | 0.03   |
| Colorful  | SL500              | 640 GB | 1       | 722   | 62    | 0.03   |
| Transcend | TS256GMTS430S      | 256 GB | 5       | 11    | 0     | 0.03   |
| China     | FPT310M8SSD128G    | 128 GB | 2       | 10    | 0     | 0.03   |
| Micron    | 1100 SATA          | 256 GB | 6       | 13    | 1     | 0.03   |
| Innodisk  | CFast 3ME3         | 128 GB | 1       | 10    | 0     | 0.03   |
| Samsung   | 470 Series SSD     | 64 GB  | 1       | 10    | 0     | 0.03   |
| Crucial   | CT480M500SSD1      | 480 GB | 3       | 1586  | 694   | 0.03   |
| Intenso   | SSD Sata III       | 240 GB | 1       | 10    | 0     | 0.03   |
| Hikvision | HS-SSD-C100 240G   | 240 GB | 1       | 10    | 0     | 0.03   |
| Lite-On   | LSS-16L6G-HP       | 16 GB  | 1       | 10    | 0     | 0.03   |
| Intel     | SSDSC2KB960G8      | 960 GB | 1       | 10    | 0     | 0.03   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 1       | 10    | 0     | 0.03   |
| Seagate   | FireCuda 120 SS... | 2 TB   | 1       | 9     | 0     | 0.03   |
| China     | SSD                | 240 GB | 2       | 9     | 0     | 0.03   |
| ZTC       | MS001-128G         | 128 GB | 1       | 9     | 0     | 0.03   |
| KingFast  | SSD                | 64 GB  | 1       | 586   | 60    | 0.03   |
| Leven     | JAJS600M512C       | 512 GB | 1       | 9     | 0     | 0.03   |
| Transcend | TS120GMTS820S      | 120 GB | 2       | 9     | 0     | 0.03   |
| Samsung   | MZ7LH480HBHQ0D3    | 480 GB | 2       | 9     | 0     | 0.02   |
| PNY       | 120GB SATA SSD     | 120 GB | 2       | 9     | 0     | 0.02   |
| ADATA     | SU760              | 1 TB   | 2       | 8     | 0     | 0.02   |
| Micron    | 1300 SATA          | 512 GB | 1       | 8     | 0     | 0.02   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 1       | 8     | 0     | 0.02   |
| KingFast  | SSD                | 240 GB | 1       | 8     | 0     | 0.02   |
| SK hynix  | HFS128G39TNF-N3A0A | 128 GB | 2       | 8     | 0     | 0.02   |
| Protectli | 64GB mSATA         | 64 GB  | 6       | 8     | 0     | 0.02   |
| Innodisk  | Corp. - mSATA 3ME3 | 16 GB  | 1       | 7     | 0     | 0.02   |
| Qunion    | SSD 128G           | 128 GB | 1       | 23    | 2     | 0.02   |
| Samsung   | SSD PM810 2.5" 7mm | 256 GB | 2       | 982   | 767   | 0.02   |
| Lite-On   | LJH-64V2G-11 M.... | 64 GB  | 1       | 38    | 4     | 0.02   |
| Innodisk  | M.2 (S80) 3MG2-P   | 992 GB | 1       | 7     | 0     | 0.02   |
| KingSpec  | Q-720              | 720 GB | 1       | 7     | 0     | 0.02   |
| Samsung   | SSD 870 EVO        | 500 GB | 2       | 7     | 0     | 0.02   |
| Lexar     | SSD                | 256 GB | 1       | 7     | 0     | 0.02   |
| China     | SSD64G             | 64 GB  | 1       | 64    | 8     | 0.02   |
| SanDisk   | SDSA6MM-008G-1006  | 8 GB   | 1       | 6     | 0     | 0.02   |
| KingSpec  | NT-512             | 512 GB | 2       | 6     | 0     | 0.02   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 2       | 6     | 0     | 0.02   |
| INDMEM    | M.2 2260           | 256 GB | 1       | 6     | 0     | 0.02   |
| Netac     | SSD                | 256 GB | 2       | 6     | 0     | 0.02   |
| KimMiDi   | T900 SSD           | 128 GB | 1       | 6     | 0     | 0.02   |
| LDLC      | SSD                | 128 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 1       | 6     | 0     | 0.02   |
| Kingston  | SKC600MS256G       | 256 GB | 6       | 5     | 0     | 0.02   |
| Transcend | TS16EPTMM1600L     | 16 GB  | 1       | 5     | 0     | 0.02   |
| SK hynix  | SC210 mSATA        | 256 GB | 2       | 248   | 75    | 0.02   |
| SMI       | SSD DISK           | 120 GB | 1       | 519   | 89    | 0.02   |
| China     | Solid              | 256 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZNLN256HMHQ-000   | 256 GB | 1       | 5     | 0     | 0.02   |
| Leven     | JAJS300M480C       | 480 GB | 1       | 5     | 0     | 0.01   |
| Intenso   | SSD                | 256 GB | 1       | 5     | 0     | 0.01   |
| HP        | SSD S600           | 240 GB | 1       | 5     | 0     | 0.01   |
| Samsung   | MZMTE128HMGR-000L2 | 128 GB | 1       | 4     | 0     | 0.01   |
| KingSpec  | KSD-SA25.7-008MJ   | 8 GB   | 1       | 4     | 0     | 0.01   |
| Seagate   | XA960LE10063       | 960 GB | 2       | 4     | 0     | 0.01   |
| XrayDisk  | SSD                | 128 GB | 1       | 4     | 0     | 0.01   |
| Zheino    | CHN mSATAM1 256    | 256 GB | 1       | 4     | 0     | 0.01   |
| Plextor   | PH6-CE240          | 240 GB | 1       | 4     | 0     | 0.01   |
| Transcend | TS64GMSA370S       | 64 GB  | 1       | 4     | 0     | 0.01   |
| Kingston  | SKC600MS512G       | 512 GB | 5       | 4     | 0     | 0.01   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 1       | 4     | 0     | 0.01   |
| Kingston  | SA400M8120G        | 120 GB | 4       | 4     | 0     | 0.01   |
| Fordisk   | 128G 6.0Gbps ND    | 128 GB | 3       | 4     | 0     | 0.01   |
| Corsair   | Neutron GTX SSD    | 120 GB | 1       | 678   | 149   | 0.01   |
| ATP       | SATA III 2.5 in... | 120 GB | 1       | 4     | 0     | 0.01   |
| Team      | T253X1240G         | 240 GB | 1       | 4     | 0     | 0.01   |
| Kingston  | OM8P0S3512F-00     | 512 GB | 1       | 4     | 0     | 0.01   |
| Mushkin   | MKNSSDSR120GB      | 120 GB | 1       | 3     | 0     | 0.01   |
| Transcend | TS256GMSA370S      | 256 GB | 2       | 3     | 0     | 0.01   |
| Innodisk  | 2.5" SATA SSD 3... | 128 GB | 1       | 3     | 0     | 0.01   |
| Kingston  | OM8P0S3128B-A0     | 128 GB | 1       | 3     | 0     | 0.01   |
| SanDisk   | SSD 128G           | 128 GB | 3       | 3     | 0     | 0.01   |
| China     | NGFF 2280 256GB... | 256 GB | 3       | 3     | 0     | 0.01   |
| Apacer    | AS220              | 256 GB | 1       | 3     | 0     | 0.01   |
| BIWIN     | SSD                | 64 GB  | 1       | 3     | 0     | 0.01   |
| Zheino    | CHN-mSATAM1-32     | 32 GB  | 1       | 3     | 0     | 0.01   |
| SanDisk   | SSD P4             | 64 GB  | 1       | 911   | 247   | 0.01   |
| Protectli | 480GB M.2          | 480 GB | 1       | 3     | 0     | 0.01   |
| Transcend | TS256GMSA452T2     | 256 GB | 2       | 3     | 0     | 0.01   |
| China     | BK-64GB MSATA SSD  | 64 GB  | 1       | 3     | 0     | 0.01   |
| Lite-On   | L8H-128V2G         | 128 GB | 1       | 3     | 0     | 0.01   |
| ORICO     | H110-120GB-PU-EP   | 120 GB | 2       | 3     | 0     | 0.01   |
| OWC       | Aura               | 960 GB | 1       | 3     | 0     | 0.01   |
| SanDisk   | SD9SB8W128G1001    | 128 GB | 1       | 3     | 0     | 0.01   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 1       | 2998  | 1010  | 0.01   |
| SanDisk   | SD8SNAT-128G-1006  | 128 GB | 1       | 2     | 0     | 0.01   |
| EMTEC     | X150               | 120 GB | 3       | 2     | 0     | 0.01   |
| Verbatim  | Vi550 S3 SSD       | 256 GB | 2       | 2     | 0     | 0.01   |
| SanDisk   | SSD 64G            | 64 GB  | 1       | 2     | 0     | 0.01   |
| INDMEM    | SSD mSATA          | 128 GB | 1       | 2     | 0     | 0.01   |
| MEMXPRO   | mSATA M3B          | 32 GB  | 4       | 2     | 0     | 0.01   |
| China     | SATA3 240GB SSD    | 240 GB | 1       | 231   | 97    | 0.01   |
| Lite-On   | LMT-32L3M          | 32 GB  | 1       | 2     | 0     | 0.01   |
| Protectli | 480GB mSATA        | 480 GB | 1       | 2     | 0     | 0.01   |
| China     | XJH-64GB           | 64 GB  | 1       | 2     | 0     | 0.01   |
| Kingston  | SNV425S264GB       | 64 GB  | 1       | 15    | 6     | 0.01   |
| AirDisk   | 128GB SSD          | 128 GB | 1       | 2     | 0     | 0.01   |
| WDC       | WDS250G2B0A        | 250 GB | 1       | 2     | 0     | 0.01   |
| ATP       | SATA III mSATA SSD | 240 GB | 5       | 2     | 0     | 0.01   |
| Intenso   | SSD                | 120 GB | 2       | 2     | 0     | 0.01   |
| Lite-On   | CV1-8B512          | 512 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MMCRE28GFMXP-MVB   | 128 GB | 1       | 2     | 0     | 0.01   |
| China     | W2EM120GDTA-S71... | 120 GB | 1       | 1     | 0     | 0.01   |
| Samsung   | MZNLH512HALU-00000 | 512 GB | 1       | 1     | 0     | 0.01   |
| Intel     | SSDSC2BA200G3T     | 200 GB | 4       | 1826  | 1028  | 0.00   |
| Netac     | SSD                | 120 GB | 3       | 1     | 0     | 0.00   |
| Smartbuy  | SSD                | 64 GB  | 1       | 1     | 0     | 0.00   |
| Pccooler  | MSATA 128G         | 128 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | SSD UM410 Serie... | 16 GB  | 1       | 38    | 24    | 0.00   |
| ATP       | SATA III M.2 22... | 240 GB | 1       | 1     | 0     | 0.00   |
| Lexar     | 128GB SSD          | 128 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZ5PA064HMCD-01000 | 64 GB  | 1       | 7     | 4     | 0.00   |
| ADATA     | SP900              | 256 GB | 1       | 606   | 424   | 0.00   |
| Transcend | TS128GMSA370S      | 128 GB | 3       | 1     | 0     | 0.00   |
| China     | sk600 128gb        | 128 GB | 1       | 1     | 0     | 0.00   |
| Wintec    | 120GB SATA3 SF2... | 120 GB | 1       | 1431  | 1017  | 0.00   |
| TCSUNBOW  | M3                 | 120 GB | 1       | 1     | 0     | 0.00   |
| China     | MSATA 64GB SSD     | 64 GB  | 1       | 1     | 0     | 0.00   |
| Seagate   | ST-MSATASSD128     | 128 GB | 1       | 1     | 0     | 0.00   |
| KingSpec  | P3-512-TM          | 512 GB | 1       | 1     | 0     | 0.00   |
| Leven     | JAJS600M128C       | 128 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | THNSNK128GCS8 SATA | 128 GB | 1       | 118   | 100   | 0.00   |
| BIWIN     | C6308              | 64 GB  | 1       | 1     | 0     | 0.00   |
| KingSpec  | P3-1TB             | 1 TB   | 1       | 1     | 0     | 0.00   |
| Yeyian    | VALK 3000          | 250 GB | 2       | 1     | 0     | 0.00   |
| Lite-On   | CS1-SP16-11 M.2... | 16 GB  | 1       | 1     | 0     | 0.00   |
| Seagate   | BarraCuda Q1 SS... | 240 GB | 1       | 1     | 0     | 0.00   |
| Dogfish   | SSD                | 32 GB  | 1       | 1     | 0     | 0.00   |
| Corsair   | CSSD-F80GBP2       | 90 GB  | 1       | 1022  | 1008  | 0.00   |
| Netac     | W800S 256GB SSD    | 256 GB | 1       | 1     | 0     | 0.00   |
| Micron    | P300-MTFDBAC050SAL | 50 GB  | 1       | 1111  | 1122  | 0.00   |
| VisionTek | mSATA              | 120 GB | 3       | 994   | 1019  | 0.00   |
| BIOSTAR   | S100-240GB         | 240 GB | 1       | 0     | 0     | 0.00   |
| Kston     | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 2       | 81    | 94    | 0.00   |
| Intel     | SSDSC1BG200G4R     | 200 GB | 2       | 922   | 1028  | 0.00   |
| FORESEE   | 512GB SSD          | 512 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSCKKR128G8      | 128 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 1       | 0     | 0     | 0.00   |
| XUM       | HX128GSSDSATA3     | 256 GB | 1       | 0     | 0     | 0.00   |
| minisf... | SSD                | 128 GB | 2       | 0     | 0     | 0.00   |
| SanDisk   | SD7UB3Q256G1001    | 256 GB | 1       | 84    | 100   | 0.00   |
| Kingston  | RBUSNS8180S3512GJ  | 512 GB | 2       | 0     | 0     | 0.00   |
| FORESEE   | 256GB SSD          | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | RBU-SNS4151S316GG2 | 16 GB  | 1       | 0     | 0     | 0.00   |
| SPCC      | M.2 SSD            | 128 GB | 1       | 0     | 0     | 0.00   |
| AMD       | R5SL120G           | 120 GB | 2       | 0     | 0     | 0.00   |
| Kingston  | RBU-SNS8350DES3... | 128 GB | 2       | 74    | 98    | 0.00   |
| HP        | SSD S700           | 250 GB | 3       | 0     | 0     | 0.00   |
| Toshiba   | THNSNK256GVN8 M... | 256 GB | 1       | 74    | 100   | 0.00   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 1       | 704   | 1023  | 0.00   |
| Intel     | SSDSC2BB120G6R     | 120 GB | 1       | 646   | 1027  | 0.00   |
| Kingsand  | C300 32G           | 32 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS16GMSA370S       | 16 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS32GMTS400S       | 32 GB  | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2BX200G4R     | 200 GB | 1       | 605   | 1027  | 0.00   |
| Integral  | V Series SATA SSD  | 120 GB | 1       | 0     | 0     | 0.00   |
| KingSpec  | P4-120             | 120 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SKC600MS1024G      | 1 TB   | 1       | 0     | 0     | 0.00   |
| ADATA     | SU650              | 960 GB | 1       | 165   | 290   | 0.00   |
| BAITITON  | BT58SSD07M         | 120 GB | 1       | 0     | 0     | 0.00   |
| China     | GM128              | 128 GB | 1       | 0     | 0     | 0.00   |
| China     | M.2 SSD            | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | OM8P0S3256B-A0     | 256 GB | 1       | 0     | 0     | 0.00   |
| ShiJi     | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS16GMSA370        | 16 GB  | 2       | 0     | 0     | 0.00   |
| KLEVV     | NEO N400 SSD       | 120 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 2       | 0     | 0     | 0.00   |
| ADATA     | SX300              | 128 GB | 2       | 21    | 525   | 0.00   |
| ATP       | SATA III M.2 22... | 480 GB | 2       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S316G       | 16 GB  | 4       | 436   | 1022  | 0.00   |
| China     | 80GB SSD           | 80 GB  | 1       | 0     | 0     | 0.00   |
| Netac     | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS512GSSD370S      | 512 GB | 1       | 0     | 0     | 0.00   |
| China     | MW02 128GB MSATA   | 128 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS128GMTS600       | 128 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TSA                | 240 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | XM13               | 32 GB  | 1       | 347   | 1029  | 0.00   |
| ADATA     | ICFS332-016GW      | 16 GB  | 1       | 0     | 0     | 0.00   |
| China     | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KB480G8      | 480 GB | 1       | 0     | 0     | 0.00   |
| Pioneer   | APS-SL3N-256       | 256 GB | 1       | 0     | 0     | 0.00   |
| QUMO      | SSD                | 120 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S316GD      | 16 GB  | 1       | 259   | 1022  | 0.00   |
| Transcend | TS32GMTS800        | 32 GB  | 1       | 0     | 0     | 0.00   |
| Kingston  | SHPM2280P2-240G    | 240 GB | 1       | 227   | 1007  | 0.00   |
| Corsair   | Force LX SSD       | 128 GB | 1       | 0     | 0     | 0.00   |
| FLEXXON   | FSSO064GTTS7-M1... | 64 GB  | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2BX100G4      | 100 GB | 1       | 0     | 0     | 0.00   |
| Pccooler  | MSATA 64G          | 64 GB  | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 860 PRO        | 2 TB   | 1       | 0     | 0     | 0.00   |
| Toshiba   | THNSNK512GVN8      | 512 GB | 1       | 137   | 692   | 0.00   |
| Seagate   | IronWolf ZA500N... | 500 GB | 2       | 0     | 0     | 0.00   |
| Zheino    | CHN-mSATAQ3-120    | 120 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | THNSNX024GMNT      | 24 GB  | 1       | 0     | 2     | 0.00   |
| Transcend | TS1TSSD230S        | 1 TB   | 2       | 0     | 0     | 0.00   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 1       | 0     | 0     | 0.00   |
| OCZ       | VERTEX             | 32 GB  | 1       | 0     | 1     | 0.00   |
| HP Phison | PSSBN032GA27MC0    | 32 GB  | 1       | 105   | 1067  | 0.00   |
| Intel     | SSDSC2KW120H6      | 120 GB | 1       | 2     | 29    | 0.00   |
| Intenso   | JAJMS600M256G      | 256 GB | 1       | 0     | 0     | 0.00   |
| KLLISRE   | SSD                | 240 GB | 1       | 0     | 0     | 0.00   |
| ShiJi     | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S332G       | 32 GB  | 1       | 79    | 1022  | 0.00   |
| SanDisk   | SD9SN8W-128G-1006  | 128 GB | 1       | 71    | 969   | 0.00   |
| Lite-On   | CV8-8E128-HP       | 128 GB | 2       | 73    | 1007  | 0.00   |
| Micron    | MTFDDAV256TDL-1... | 256 GB | 1       | 45    | 1008  | 0.00   |
| China     | XJH-32GB           | 32 GB  | 1       | 0     | 0     | 0.00   |
| INDMEM    | M.2 2280           | 64 GB  | 1       | 0     | 0     | 0.00   |
| Integral  | V Series SATA SSD  | 240 GB | 1       | 0     | 0     | 0.00   |
| KingFast  | SSD                | 1 TB   | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD8SFAT064G1122    | 64 GB  | 1       | 0     | 0     | 0.00   |
| Seagate   | FireCuda 120 SS... | 500 GB | 1       | 0     | 0     | 0.00   |
| Terabit   | T50S3STMLC-256G    | 256 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS32GMSA370S       | 32 GB  | 1       | 0     | 0     | 0.00   |
| Valuetech | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WDS500G1R0A-68A4W0 | 500 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KW480H6      | 480 GB | 1       | 39    | 1010  | 0.00   |
| Intel     | SSDSC2BF240A5      | 240 GB | 1       | 74    | 2017  | 0.00   |
| Lexar     | CFAST 64GB CARD    | 64 GB  | 1       | 0     | 6     | 0.00   |
| SMI       | SSD DISK           | 506 GB | 1       | 44    | 2329  | 0.00   |
| Micron    | MTFDDAT128MAM-1J2  | 128 GB | 1       | 28    | 1587  | 0.00   |
| ADATA     | SP550              | 480 GB | 1       | 4     | 1194  | 0.00   |
| SSSTC     | CVB-8D128-HP       | 128 GB | 1       | 3     | 1008  | 0.00   |
| GLOWAY    | FER60GS3-S7        | 64 GB  | 1       | 2     | 1168  | 0.00   |

SSD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| G.Skill   | Unknown                | 1      | 1       | 2532  | 0     | 6.94   |
| Toshiba   | OCZ/Toshiba Trion SSDs | 1      | 1       | 1746  | 0     | 4.79   |
| Crucial   | RealSSD m4/C400        | 1      | 2       | 1581  | 0     | 4.33   |
| Intel     | 525 Series SSDs        | 3      | 7       | 1423  | 1     | 3.79   |
| AMD       | Silicon Motion base... | 1      | 2       | 1341  | 0     | 3.68   |
| Crucial   | RealSSD m4/C400/P400   | 6      | 24      | 1486  | 85    | 3.65   |
| Micro ... | Unknown                | 1      | 1       | 1297  | 0     | 3.55   |
| SuperM... | Unknown                | 1      | 1       | 1295  | 0     | 3.55   |
| ADATA     | JMicron based SSDs     | 4      | 6       | 1272  | 0     | 3.49   |
| Seagate   | Nytro XF1230 SATA SSD  | 1      | 2       | 1266  | 0     | 3.47   |
| Intel     | 320 Series SSDs        | 9      | 27      | 1240  | 2     | 3.34   |
| Dell      | Certified Intel S35... | 1      | 2       | 1173  | 0     | 3.22   |
| Intel     | Dell Certified Inte... | 2      | 11      | 1096  | 0     | 3.00   |
| OCZ       | SandForce Driven SSDs  | 15     | 32      | 1287  | 44    | 2.98   |
| Mushkin   | SandForce Driven SSDs  | 3      | 3       | 1057  | 0     | 2.90   |
| Crucial   | Unknown                | 1      | 2       | 1042  | 0     | 2.86   |
| Transcend | JMicron/Maxiotek ba... | 3      | 6       | 1029  | 0     | 2.82   |
| HPE       | Unknown                | 6      | 11      | 1025  | 1     | 2.75   |
| ADATA     | JMicron/Maxiotek ba... | 2      | 3       | 1002  | 0     | 2.75   |
| OCZ       | Indilinx Barefoot_2... | 7      | 11      | 1027  | 1     | 2.57   |
| Intel     | 730 and DC S35x0/36... | 20     | 46      | 1141  | 135   | 2.49   |
| Intel     | 330/335 Series SSDs    | 5      | 13      | 1364  | 2     | 2.40   |
| Intel     | S3520 Series SSDs      | 2      | 3       | 1246  | 1     | 2.35   |
| Silico... | Unknown                | 1      | 1       | 828   | 0     | 2.27   |
| Goodram   | Phison Driven OEM SSDs | 2      | 8       | 827   | 0     | 2.27   |
| Toshiba   | HG3 Series             | 1      | 1       | 826   | 0     | 2.26   |
| Micron    | 5100 Pro / 5200 SSDs   | 1      | 4       | 778   | 0     | 2.13   |
| Toshiba   | HG5d Series            | 2      | 2       | 777   | 0     | 2.13   |
| Toshiba   | HG6 Series SSD         | 5      | 11      | 770   | 0     | 2.11   |
| Corsair   | SandForce Driven SSDs  | 13     | 26      | 1035  | 79    | 2.04   |
| Intel     | 520 Series SSDs        | 7      | 23      | 1463  | 398   | 2.00   |
| Toshiba   | HG5 Series             | 1      | 1       | 709   | 0     | 1.94   |
| ADATA     | SandForce Driven SSDs  | 5      | 10      | 760   | 43    | 1.92   |
| Apple     | JMicron based SSDs     | 2      | 3       | 695   | 0     | 1.91   |
| Toshiba   | JMicron/Maxiotek ba... | 1      | 1       | 692   | 0     | 1.90   |
| Kingston  | SandForce Driven SSDs  | 15     | 103     | 918   | 21    | 1.87   |
| Samsung   | Unknown                | 16     | 20      | 717   | 2     | 1.86   |
| V-GeN     | Unknown                | 2      | 2       | 639   | 0     | 1.75   |
| Mach X... | Unknown                | 1      | 1       | 629   | 0     | 1.73   |
| Phison    | Phison Driven SSDs     | 1      | 1       | 628   | 0     | 1.72   |
| Samsung   | Samsung based SSDs     | 153    | 755     | 627   | 7     | 1.63   |
| OCZ       | Indilinx Barefoot 3... | 2      | 4       | 674   | 1     | 1.59   |
| Kingston  | SSDNow UV400           | 1      | 1       | 566   | 0     | 1.55   |
| Intel     | X25-E SSDs             | 2      | 3       | 538   | 0     | 1.48   |
| SanDisk   | SanDisk based SSDs     | 20     | 66      | 557   | 2     | 1.47   |
| Intel     | X18-M/X25-M/X25-V G... | 7      | 17      | 1805  | 8     | 1.34   |
| Phison    | Driven OEM SSDs        | 8      | 67      | 487   | 0     | 1.34   |
| Intel     | 53x and Pro 1500/25... | 13     | 37      | 530   | 84    | 1.30   |
| Advantech | Unknown                | 4      | 6       | 472   | 0     | 1.30   |
| Toshiba   | Unknown                | 20     | 29      | 480   | 31    | 1.29   |
| Crucial   | BX/MX1/2/3/500, M5/... | 8      | 37      | 619   | 2     | 1.28   |
| Innodisk  | Unknown                | 7      | 8       | 462   | 0     | 1.27   |
| Delkin... | Unknown                | 1      | 1       | 916   | 1     | 1.26   |
| CWDISK    | Unknown                | 1      | 1       | 455   | 0     | 1.25   |
| SanDisk   | SandForce Driven SSDs  | 3      | 39      | 480   | 21    | 1.24   |
| Apacer    | SDM4 Series SSD Module | 2      | 16      | 523   | 14    | 1.24   |
| SuperM... | Silicon Motion base... | 2      | 3       | 450   | 0     | 1.23   |
| KingFast  | Silicon Motion base... | 2      | 6       | 450   | 0     | 1.23   |
| China     | Phison Driven OEM SSDs | 6      | 69      | 470   | 2     | 1.23   |
| AEGO      | Unknown                | 1      | 1       | 445   | 0     | 1.22   |
| Goodram   | Phison Driven SSDs     | 4      | 5       | 433   | 0     | 1.19   |
| SATADOM   | Unknown                | 1      | 1       | 425   | 0     | 1.16   |
| KST       | Unknown                | 1      | 1       | 416   | 0     | 1.14   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 1      | 1       | 411   | 0     | 1.13   |
| HP        | Unknown                | 8      | 11      | 398   | 0     | 1.09   |
| PNY       | Phison Driven SSDs     | 5      | 36      | 395   | 0     | 1.08   |
| Plextor   | Unknown                | 6      | 6       | 408   | 1     | 1.05   |
| Apacer    | SDM5/5A/5A-M Series... | 2      | 8       | 778   | 136   | 1.04   |
| Vaseky    | Unknown                | 4      | 4       | 373   | 0     | 1.02   |
| Toshiba   | OCZ                    | 2      | 2       | 368   | 0     | 1.01   |
| Team      | Silicon Motion base... | 2      | 2       | 367   | 0     | 1.01   |
| AVEXIR    | Unknown                | 1      | 1       | 365   | 0     | 1.00   |
| Micron    | 5100 Pro / 52x0 / 5... | 2      | 3       | 364   | 0     | 1.00   |
| SanDisk   | Marvell based SanDi... | 39     | 117     | 404   | 2     | 0.99   |
| MyDigi... | Unknown                | 2      | 3       | 643   | 3     | 0.97   |
| Transcend | JMicron based SSDs     | 1      | 2       | 351   | 0     | 0.96   |
| Intel     | 545s Series SSDs       | 4      | 17      | 355   | 1     | 0.96   |
| Micron    | BX/MX1/2/3/500, M5/... | 5      | 14      | 347   | 1     | 0.95   |
| DST       | Unknown                | 1      | 1       | 345   | 0     | 0.95   |
| OCZ       | OCZ/Toshiba Trion SSDs | 2      | 3       | 341   | 0     | 0.93   |
| TCSUNBOW  | Unknown                | 2      | 5       | 336   | 0     | 0.92   |
| OWC       | SandForce Driven SSDs  | 4      | 10      | 334   | 0     | 0.92   |
| Micron    | Client SSDs            | 9      | 16      | 340   | 1     | 0.91   |
| Mushkin   | Unknown                | 4      | 4       | 328   | 0     | 0.90   |
| Kingston  | SSDNow UV400/500       | 9      | 109     | 322   | 1     | 0.87   |
| Intel     | Unknown                | 19     | 29      | 416   | 79    | 0.85   |
| Hoodisk   | Unknown                | 1      | 3       | 308   | 0     | 0.84   |
| Hoodisk   | Phison Driven OEM SSDs | 5      | 124     | 307   | 0     | 0.84   |
| Smartbuy  | Phison Driven SSDs     | 4      | 5       | 306   | 0     | 0.84   |
| Hyundai   | Unknown                | 1      | 1       | 306   | 0     | 0.84   |
| SK hynix  | SATA SSDs              | 10     | 20      | 355   | 19    | 0.80   |
| Apple     | SD/SM/TS E/F/G SSDs    | 8      | 16      | 357   | 8     | 0.79   |
| KIOXIA... | Unknown                | 1      | 1       | 286   | 0     | 0.78   |
| SanDisk   | Unknown                | 57     | 84      | 315   | 27    | 0.77   |
| SMART     | Unknown                | 1      | 1       | 280   | 0     | 0.77   |
| Plextor   | M3/M5/M6/M7 Series ... | 9      | 12      | 354   | 1     | 0.75   |
| Apple     | Unknown                | 2      | 2       | 268   | 0     | 0.74   |
| Corsair   | Indilinx Barefoot b... | 2      | 2       | 262   | 0     | 0.72   |
| SPCC      | Phison Driven OEM SSDs | 7      | 70      | 256   | 1     | 0.70   |
| Gigabyte  | Unknown                | 1      | 2       | 252   | 0     | 0.69   |
| SK hynix  | Unknown                | 8      | 13      | 293   | 25    | 0.68   |
| Seagate   | IronWolf 110 SATA SSD  | 1      | 1       | 240   | 0     | 0.66   |
| Patriot   | Unknown                | 3      | 3       | 239   | 0     | 0.66   |
| Crucial   | BX/MX1/2/3/500, M5/... | 1      | 5       | 735   | 4     | 0.65   |
| Ramaxel   | Unknown                | 1      | 1       | 235   | 0     | 0.65   |
| Seagate   | Unknown                | 11     | 13      | 301   | 1     | 0.64   |
| ASENNO    | Unknown                | 1      | 1       | 231   | 0     | 0.63   |
| Micron    | Unknown                | 12     | 17      | 288   | 219   | 0.60   |
| Team      | Unknown                | 5      | 5       | 217   | 0     | 0.60   |
| Kingston  | JMicron/Maxiotek ba... | 4      | 4       | 893   | 5     | 0.59   |
| Kingston  | Unknown                | 31     | 50      | 270   | 127   | 0.59   |
| Patriot   | Phison Driven SSDs     | 4      | 18      | 206   | 0     | 0.57   |
| ADATA     | Unknown                | 17     | 37      | 224   | 57    | 0.57   |
| Kingston  | Phison Driven SSDs     | 13     | 191     | 200   | 1     | 0.55   |
| WDC       | Blue / Red / Green ... | 24     | 135     | 200   | 1     | 0.53   |
| Innodisk  | 1IE3/3IE3/3ME3/3IE4... | 3      | 3       | 180   | 0     | 0.50   |
| Intel     | Dell Certified Inte... | 2      | 3       | 178   | 0     | 0.49   |
| KingDian  | Unknown                | 1      | 1       | 177   | 0     | 0.49   |
| Mushkin   | Silicon Motion base... | 3      | 4       | 174   | 0     | 0.48   |
| Corsair   | Unknown                | 4      | 4       | 340   | 38    | 0.47   |
| Crucial   | Client SSDs            | 26     | 244     | 225   | 30    | 0.47   |
| Apacer    | Unknown                | 11     | 16      | 217   | 1     | 0.44   |
| Indilinx  | Unknown                | 2      | 2       | 157   | 0     | 0.43   |
| Intel     | S4510/S4610/S4500/S... | 6      | 31      | 149   | 0     | 0.41   |
| WDC       | Blue and Green SSDs    | 5      | 40      | 172   | 1     | 0.41   |
| Intenso   | Unknown                | 11     | 25      | 147   | 3     | 0.40   |
| KingSpec  | JMicron/Maxiotek ba... | 4      | 9       | 145   | 0     | 0.40   |
| Transcend | Unknown                | 15     | 34      | 143   | 31    | 0.36   |
| Faspeed   | Unknown                | 2      | 5       | 129   | 0     | 0.36   |
| XrayDisk  | Unknown                | 2      | 2       | 128   | 0     | 0.35   |
| Goodram   | Unknown                | 7      | 15      | 127   | 0     | 0.35   |
| KingSpec  | Unknown                | 12     | 16      | 123   | 0     | 0.34   |
| ADATA     | Silicon Motion base... | 11     | 44      | 168   | 64    | 0.33   |
| Lite-On   | Unknown                | 29     | 35      | 125   | 58    | 0.33   |
| KingDian  | Silicon Motion base... | 5      | 8       | 117   | 127   | 0.32   |
| Apple     | MacBook Air SSD        | 1      | 1       | 113   | 0     | 0.31   |
| Micron    | RealSSD m4/C400/P400   | 4      | 8       | 118   | 127   | 0.31   |
| Dogfish   | Unknown                | 6      | 9       | 136   | 1     | 0.31   |
| KingFast  | Unknown                | 7      | 26      | 130   | 38    | 0.30   |
| XUNZHE    | Unknown                | 1      | 1       | 106   | 0     | 0.29   |
| Transcend | Silicon Motion base... | 40     | 180     | 103   | 0     | 0.28   |
| Kston     | Unknown                | 4      | 17      | 116   | 1     | 0.28   |
| Zheino    | Unknown                | 7      | 8       | 101   | 0     | 0.28   |
| BlueRay   | Unknown                | 1      | 1       | 95    | 0     | 0.26   |
| Pioneer   | Unknown                | 2      | 2       | 94    | 0     | 0.26   |
| Intenso   | Silicon Motion base... | 2      | 3       | 94    | 0     | 0.26   |
| BIWIN     | Unknown                | 5      | 19      | 142   | 14    | 0.26   |
| Ramsta    | Unknown                | 1      | 1       | 91    | 0     | 0.25   |
| SPCC      | Unknown                | 3      | 5       | 90    | 0     | 0.25   |
| China     | Unknown                | 51     | 75      | 96    | 2     | 0.25   |
| PNY       | Unknown                | 6      | 11      | 83    | 0     | 0.23   |
| UDinfo    | Unknown                | 1      | 3       | 82    | 0     | 0.23   |
| Protectli | Unknown                | 8      | 34      | 80    | 0     | 0.22   |
| Apacer    | AS340 SSDs             | 2      | 2       | 72    | 0     | 0.20   |
| Micron    | BX/MX1/2/3/500, M5/... | 1      | 4       | 1695  | 270   | 0.19   |
| ZTC       | Unknown                | 2      | 3       | 399   | 9     | 0.19   |
| Apacer    | SSDs                   | 2      | 3       | 68    | 0     | 0.19   |
| Drevo     | Silicon Motion base... | 2      | 3       | 66    | 0     | 0.18   |
| AMD       | Unknown                | 2      | 5       | 90    | 4     | 0.18   |
| Plextor   | M3/M5/M6 Series SSDs   | 1      | 2       | 64    | 0     | 0.18   |
| Dogfish   | Silicon Motion base... | 3      | 23      | 72    | 1     | 0.17   |
| Intel     | 311/313 Series SSDs    | 1      | 1       | 63    | 0     | 0.17   |
| LDLC      | Unknown                | 2      | 2       | 60    | 0     | 0.16   |
| Intel     | 510 Series SSDs        | 1      | 2       | 57    | 0     | 0.16   |
| Gigabyte  | Phison Driven SSDs     | 2      | 10      | 57    | 0     | 0.16   |
| Transcend | SandForce Driven SSDs  | 1      | 2       | 170   | 3     | 0.16   |
| EMTEC     | Unknown                | 3      | 5       | 53    | 0     | 0.15   |
| Intenso   | Phison Driven OEM SSDs | 2      | 9       | 53    | 0     | 0.15   |
| FORESEE   | Unknown                | 5      | 46      | 53    | 0     | 0.15   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 1      | 6       | 52    | 0     | 0.14   |
| Lenovo    | Unknown                | 1      | 1       | 50    | 0     | 0.14   |
| ATP       | Unknown                | 6      | 14      | 47    | 0     | 0.13   |
| Netac     | Unknown                | 7      | 10      | 41    | 0     | 0.11   |
| Verbatim  | Unknown                | 2      | 3       | 40    | 0     | 0.11   |
| Fujitsu   | Unknown                | 1      | 1       | 35    | 0     | 0.10   |
| minisf... | Unknown                | 2      | 9       | 33    | 0     | 0.09   |
| MidasF... | Unknown                | 1      | 1       | 32    | 0     | 0.09   |
| Hikvision | Unknown                | 3      | 3       | 26    | 0     | 0.07   |
| WDC       | Unknown                | 1      | 1       | 24    | 0     | 0.07   |
| Kingston  | Silicon Motion base... | 1      | 2       | 22    | 0     | 0.06   |
| BR        | Unknown                | 1      | 1       | 22    | 0     | 0.06   |
| OCZ       | Indilinx Barefoot b... | 2      | 3       | 199   | 38    | 0.06   |
| SanPin    | Unknown                | 1      | 1       | 19    | 0     | 0.05   |
| MicroD... | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| Lexar     | Unknown                | 4      | 7       | 16    | 1     | 0.05   |
| SETHRISE  | Unknown                | 1      | 1       | 14    | 0     | 0.04   |
| Lite-On   | Silicon Motion base... | 1      | 1       | 13    | 0     | 0.04   |
| NTC       | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| Colorful  | Unknown                | 1      | 1       | 722   | 62    | 0.03   |
| Qunion    | Unknown                | 2      | 2       | 17    | 1     | 0.03   |
| ORICO     | Unknown                | 2      | 3       | 8     | 0     | 0.02   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 1      | 1       | 7     | 0     | 0.02   |
| KimMiDi   | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| Leven     | Unknown                | 3      | 3       | 5     | 0     | 0.01   |
| Seagate   | Nytro SATA SSD         | 1      | 2       | 4     | 0     | 0.01   |
| Fordisk   | Unknown                | 1      | 3       | 4     | 0     | 0.01   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 1      | 1       | 3     | 0     | 0.01   |
| OWC       | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| INDMEM    | Unknown                | 3      | 3       | 2     | 0     | 0.01   |
| SMI       | Unknown                | 2      | 2       | 282   | 1209  | 0.01   |
| MEMXPRO   | Unknown                | 1      | 4       | 2     | 0     | 0.01   |
| AirDisk   | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| Wintec    | Unknown                | 1      | 1       | 1431  | 1017  | 0.00   |
| TCSUNBOW  | Silicon Motion base... | 1      | 1       | 1     | 0     | 0.00   |
| Yeyian    | Unknown                | 1      | 2       | 1     | 0     | 0.00   |
| VisionTek | Unknown                | 1      | 3       | 994   | 1019  | 0.00   |
| BIOSTAR   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Pccooler  | Unknown                | 2      | 2       | 0     | 0     | 0.00   |
| XUM       | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Kingsand  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| BAITITON  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| KLEVV     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Integral  | Unknown                | 2      | 2       | 0     | 0     | 0.00   |
| ShiJi     | Unknown                | 2      | 2       | 0     | 0     | 0.00   |
| QUMO      | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| FLEXXON   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison | Unknown                | 1      | 1       | 105   | 1067  | 0.00   |
| KLLISRE   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Intel     | 540 Series SSDs        | 2      | 2       | 20    | 520   | 0.00   |
| Terabit   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Valuetech | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| SSSTC     | Unknown                | 1      | 1       | 3     | 1008  | 0.00   |
| GLOWAY    | Unknown                | 1      | 1       | 2     | 1168  | 0.00   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| G.Skill     | 1      | 1       | 2532  | 0     | 6.94   |
| Micro Ce... | 1      | 1       | 1297  | 0     | 3.55   |
| Dell        | 1      | 2       | 1173  | 0     | 3.22   |
| HPE         | 6      | 11      | 1025  | 1     | 2.75   |
| OCZ         | 28     | 53      | 1072  | 29    | 2.51   |
| Silicon ... | 1      | 1       | 828   | 0     | 2.27   |
| SuperMicro  | 3      | 4       | 661   | 0     | 1.81   |
| Corsair     | 19     | 32      | 900   | 69    | 1.76   |
| Intel       | 105    | 272     | 877   | 81    | 1.76   |
| V-GeN       | 2      | 2       | 639   | 0     | 1.75   |
| Mach Xtreme | 1      | 1       | 629   | 0     | 1.73   |
| Samsung     | 169    | 775     | 629   | 6     | 1.64   |
| Toshiba     | 33     | 48      | 597   | 19    | 1.62   |
| Phison      | 9      | 68      | 489   | 0     | 1.34   |
| Advantech   | 4      | 6       | 472   | 0     | 1.30   |
| Mushkin     | 10     | 11      | 471   | 0     | 1.29   |
| Delkin D... | 1      | 1       | 916   | 1     | 1.26   |
| CWDISK      | 1      | 1       | 455   | 0     | 1.25   |
| AEGO        | 1      | 1       | 445   | 0     | 1.22   |
| AMD         | 3      | 7       | 448   | 3     | 1.18   |
| KST         | 1      | 1       | 416   | 0     | 1.14   |
| HP          | 8      | 11      | 398   | 0     | 1.09   |
| SanDisk     | 119    | 306     | 422   | 11    | 1.07   |
| Goodram     | 13     | 28      | 381   | 0     | 1.05   |
| Vaseky      | 4      | 4       | 373   | 0     | 1.02   |
| AVEXIR      | 1      | 1       | 365   | 0     | 1.00   |
| MyDigita... | 2      | 3       | 643   | 3     | 0.97   |
| DST         | 1      | 1       | 345   | 0     | 0.95   |
| Kingston    | 74     | 460     | 403   | 19    | 0.93   |
| Apple       | 13     | 22      | 384   | 6     | 0.91   |
| Innodisk    | 13     | 14      | 333   | 0     | 0.91   |
| Seagate     | 14     | 18      | 372   | 1     | 0.89   |
| PNY         | 11     | 47      | 322   | 0     | 0.88   |
| Crucial     | 43     | 314     | 390   | 30    | 0.85   |
| Hoodisk     | 6      | 127     | 307   | 0     | 0.84   |
| Smartbuy    | 4      | 5       | 306   | 0     | 0.84   |
| Hyundai     | 1      | 1       | 306   | 0     | 0.84   |
| ADATA       | 39     | 100     | 339   | 54    | 0.84   |
| OWC         | 5      | 11      | 304   | 0     | 0.83   |
| Apacer      | 19     | 45      | 409   | 30    | 0.80   |
| Micron      | 34     | 66      | 411   | 89    | 0.80   |
| KIOXIA-E... | 1      | 1       | 286   | 0     | 0.78   |
| Plextor     | 16     | 20      | 341   | 1     | 0.78   |
| SMART       | 1      | 1       | 280   | 0     | 0.77   |
| TCSUNBOW    | 3      | 6       | 280   | 0     | 0.77   |
| SK hynix    | 18     | 33      | 330   | 22    | 0.75   |
| China       | 57     | 144     | 275   | 2     | 0.72   |
| Team        | 7      | 7       | 260   | 0     | 0.71   |
| SPCC        | 10     | 75      | 245   | 1     | 0.67   |
| Ramaxel     | 1      | 1       | 235   | 0     | 0.65   |
| ASENNO      | 1      | 1       | 231   | 0     | 0.63   |
| Patriot     | 7      | 21      | 211   | 0     | 0.58   |
| WDC         | 30     | 176     | 193   | 1     | 0.50   |
| KingFast    | 9      | 32      | 190   | 31    | 0.47   |
| Indilinx    | 2      | 2       | 157   | 0     | 0.43   |
| Transcend   | 60     | 224     | 136   | 5     | 0.37   |
| KingSpec    | 16     | 25      | 131   | 0     | 0.36   |
| Faspeed     | 2      | 5       | 129   | 0     | 0.36   |
| XrayDisk    | 2      | 2       | 128   | 0     | 0.35   |
| KingDian    | 6      | 9       | 123   | 113   | 0.33   |
| Intenso     | 15     | 37      | 120   | 2     | 0.33   |
| Lite-On     | 30     | 36      | 122   | 57    | 0.32   |
| XUNZHE      | 1      | 1       | 106   | 0     | 0.29   |
| SATADOM     | 2      | 7       | 105   | 0     | 0.29   |
| Kston       | 4      | 17      | 116   | 1     | 0.28   |
| Zheino      | 7      | 8       | 101   | 0     | 0.28   |
| BlueRay     | 1      | 1       | 95    | 0     | 0.26   |
| Pioneer     | 2      | 2       | 94    | 0     | 0.26   |
| BIWIN       | 5      | 19      | 142   | 14    | 0.26   |
| Ramsta      | 1      | 1       | 91    | 0     | 0.25   |
| Gigabyte    | 3      | 12      | 89    | 0     | 0.25   |
| UDinfo      | 1      | 3       | 82    | 0     | 0.23   |
| Protectli   | 8      | 34      | 80    | 0     | 0.22   |
| Dogfish     | 9      | 32      | 90    | 1     | 0.21   |
| ZTC         | 2      | 3       | 399   | 9     | 0.19   |
| Drevo       | 2      | 3       | 66    | 0     | 0.18   |
| LDLC        | 2      | 2       | 60    | 0     | 0.16   |
| EMTEC       | 3      | 5       | 53    | 0     | 0.15   |
| FORESEE     | 5      | 46      | 53    | 0     | 0.15   |
| Lenovo      | 1      | 1       | 50    | 0     | 0.14   |
| ATP         | 6      | 14      | 47    | 0     | 0.13   |
| Netac       | 7      | 10      | 41    | 0     | 0.11   |
| Verbatim    | 2      | 3       | 40    | 0     | 0.11   |
| Fujitsu     | 1      | 1       | 35    | 0     | 0.10   |
| minisforum  | 2      | 9       | 33    | 0     | 0.09   |
| MidasForce  | 1      | 1       | 32    | 0     | 0.09   |
| Hikvision   | 3      | 3       | 26    | 0     | 0.07   |
| BR          | 1      | 1       | 22    | 0     | 0.06   |
| SanPin      | 1      | 1       | 19    | 0     | 0.05   |
| MicroDream  | 1      | 1       | 18    | 0     | 0.05   |
| Lexar       | 4      | 7       | 16    | 1     | 0.05   |
| SETHRISE    | 1      | 1       | 14    | 0     | 0.04   |
| NTC         | 1      | 1       | 12    | 0     | 0.03   |
| Colorful    | 1      | 1       | 722   | 62    | 0.03   |
| Qunion      | 2      | 2       | 17    | 1     | 0.03   |
| ORICO       | 2      | 3       | 8     | 0     | 0.02   |
| KimMiDi     | 1      | 1       | 6     | 0     | 0.02   |
| Leven       | 3      | 3       | 5     | 0     | 0.01   |
| Fordisk     | 1      | 3       | 4     | 0     | 0.01   |
| INDMEM      | 3      | 3       | 2     | 0     | 0.01   |
| SMI         | 2      | 2       | 282   | 1209  | 0.01   |
| MEMXPRO     | 1      | 4       | 2     | 0     | 0.01   |
| AirDisk     | 1      | 1       | 2     | 0     | 0.01   |
| Wintec      | 1      | 1       | 1431  | 1017  | 0.00   |
| Yeyian      | 1      | 2       | 1     | 0     | 0.00   |
| VisionTek   | 1      | 3       | 994   | 1019  | 0.00   |
| BIOSTAR     | 1      | 1       | 0     | 0     | 0.00   |
| Pccooler    | 2      | 2       | 0     | 0     | 0.00   |
| XUM         | 1      | 1       | 0     | 0     | 0.00   |
| Kingsand    | 1      | 1       | 0     | 0     | 0.00   |
| BAITITON    | 1      | 1       | 0     | 0     | 0.00   |
| KLEVV       | 1      | 1       | 0     | 0     | 0.00   |
| Integral    | 2      | 2       | 0     | 0     | 0.00   |
| ShiJi       | 2      | 2       | 0     | 0     | 0.00   |
| QUMO        | 1      | 1       | 0     | 0     | 0.00   |
| FLEXXON     | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison   | 1      | 1       | 105   | 1067  | 0.00   |
| KLLISRE     | 1      | 1       | 0     | 0     | 0.00   |
| Terabit     | 1      | 1       | 0     | 0     | 0.00   |
| Valuetech   | 1      | 1       | 0     | 0     | 0.00   |
| SSSTC       | 1      | 1       | 3     | 1008  | 0.00   |
| GLOWAY      | 1      | 1       | 2     | 1168  | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See full list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Intel     | SSDPEDMW400G4      | 400 GB | 2       | 1410  | 0     | 3.86   |
| Samsung   | SSD 950 PRO        | 512 GB | 3       | 1332  | 0     | 3.65   |
| Plextor   | PX-256M8PeY        | 256 GB | 1       | 1218  | 0     | 3.34   |
| Intel     | SSDPEDME016T4S     | 1.6 TB | 1       | 1203  | 0     | 3.30   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 1       | 1195  | 0     | 3.28   |
| Intel     | SSDPED1D280GA      | 280 GB | 1       | 1099  | 0     | 3.01   |
| Kingston  | SKC1000240G        | 240 GB | 1       | 934   | 0     | 2.56   |
| Samsung   | MZVPV256HDGL-000L7 | 256 GB | 1       | 915   | 0     | 2.51   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 1       | 827   | 0     | 2.27   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 2       | 765   | 0     | 2.10   |
| Samsung   | SSD 950 PRO        | 256 GB | 1       | 1495  | 1     | 2.05   |
| Transcend | TS256GMTE110S      | 256 GB | 1       | 730   | 0     | 2.00   |
| HP        | SSD EX900          | 120 GB | 2       | 637   | 0     | 1.75   |
| Plextor   | PX-256M8PeG        | 256 GB | 1       | 598   | 0     | 1.64   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 3       | 561   | 0     | 1.54   |
| Samsung   | MZFLV512HCJH-000MV | 512 GB | 1       | 554   | 0     | 1.52   |
| HP        | SSD EX920          | 512 GB | 1       | 531   | 0     | 1.46   |
| Phison    | Sabrent Rocket 4.0 | 500 GB | 1       | 510   | 0     | 1.40   |
| Patriot   | Scorch M2          | 128 GB | 1       | 493   | 0     | 1.35   |
| Intel     | SSDPEKKW128G8      | 128 GB | 2       | 489   | 0     | 1.34   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 1       | 446   | 0     | 1.22   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 2       | 429   | 0     | 1.18   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 2       | 415   | 0     | 1.14   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 2       | 380   | 0     | 1.04   |
| SPCC      | M.2 PCIE SSD       | 256 GB | 1       | 376   | 0     | 1.03   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 1       | 367   | 0     | 1.01   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 1       | 363   | 0     | 1.00   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 1       | 363   | 0     | 1.00   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 1       | 338   | 0     | 0.93   |
| Corsair   | Force MP600        | 2 TB   | 2       | 336   | 0     | 0.92   |
| Samsung   | SSD 960 EVO        | 250 GB | 18      | 334   | 0     | 0.92   |
| ADATA     | SX6000NP           | 128 GB | 2       | 324   | 0     | 0.89   |
| ADATA     | SX8200PNP          | 1 TB   | 8       | 306   | 0     | 0.84   |
| Intel     | SSDPED1D480GA      | 480 GB | 1       | 299   | 0     | 0.82   |
| Kingston  | SA1000M8240G       | 240 GB | 1       | 298   | 0     | 0.82   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 2       | 297   | 0     | 0.81   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 1       | 293   | 0     | 0.80   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 1       | 289   | 0     | 0.79   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 1       | 286   | 0     | 0.78   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 1       | 284   | 0     | 0.78   |
| Samsung   | SSD 970 PRO        | 512 GB | 10      | 282   | 0     | 0.77   |
| Samsung   | SSD 970 EVO        | 250 GB | 11      | 278   | 0     | 0.76   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 4       | 278   | 0     | 0.76   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 1       | 277   | 0     | 0.76   |
| WDC       | WDBA3V0010BNC-WRSN | 1 TB   | 1       | 276   | 0     | 0.76   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 2       | 265   | 0     | 0.73   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 259   | 0     | 0.71   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 1       | 258   | 0     | 0.71   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 1       | 257   | 0     | 0.71   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 255   | 0     | 0.70   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 2       | 255   | 0     | 0.70   |
| Transcend | TS128GMTE110S      | 128 GB | 2       | 253   | 0     | 0.69   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 1       | 245   | 0     | 0.67   |
| Crucial   | CT500P1SSD8        | 500 GB | 6       | 241   | 0     | 0.66   |
| Phison    | PCIe SSD           | 500 GB | 5       | 231   | 0     | 0.64   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 3       | 227   | 0     | 0.62   |
| Samsung   | SSD 960 EVO        | 500 GB | 8       | 225   | 0     | 0.62   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 3       | 221   | 0     | 0.61   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 1       | 218   | 0     | 0.60   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 218   | 0     | 0.60   |
| Silico... | R5MP240G8          | 240 GB | 1       | 218   | 0     | 0.60   |
| KIOXIA    | KBG40ZNS128G NVMe  | 128 GB | 1       | 217   | 0     | 0.60   |
| Intel     | SSDPE21D280GA      | 280 GB | 2       | 217   | 0     | 0.60   |
| Samsung   | PM951 NVMe         | 256 GB | 2       | 217   | 0     | 0.59   |
| Silico... | Asgard AN2 500N... | 500 GB | 1       | 216   | 0     | 0.59   |
| Transcend | TS500GMTE240S      | 500 GB | 2       | 214   | 0     | 0.59   |
| Phison    | Viper M.2 VPN100   | 256 GB | 1       | 208   | 0     | 0.57   |
| Samsung   | MZVLB1T0HALR-000L2 | 1 TB   | 1       | 208   | 0     | 0.57   |
| KIOXIA    | KBG40ZPZ512G NVMe  | 512 GB | 1       | 207   | 0     | 0.57   |
| Samsung   | SSD 970 EVO        | 2 TB   | 1       | 205   | 0     | 0.56   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 3       | 200   | 0     | 0.55   |
| Intel     | SSDPEKKW256G8      | 256 GB | 2       | 198   | 0     | 0.54   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 5       | 198   | 0     | 0.54   |
| Mushkin   | MKNSSDPE500GB-D8   | 500 GB | 1       | 195   | 0     | 0.54   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 3       | 193   | 0     | 0.53   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 7       | 192   | 0     | 0.53   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 3       | 191   | 0     | 0.53   |
| Toshiba   | KXG50PNV2T04 NVMe  | 2 TB   | 1       | 188   | 0     | 0.52   |
| Phison    | Sabrent Rocket 4.0 | 2 TB   | 1       | 185   | 0     | 0.51   |
| ADATA     | SX8200PNP          | 2 TB   | 1       | 181   | 0     | 0.50   |
| Kingston  | RBUSNS8154P3256GJ3 | 256 GB | 1       | 175   | 0     | 0.48   |
| Phison    | Sabrent            | 1 TB   | 12      | 174   | 0     | 0.48   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 1       | 172   | 0     | 0.47   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 1       | 172   | 0     | 0.47   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 5       | 172   | 0     | 0.47   |
| Toshiba   | KBG30ZMV512G       | 512 GB | 1       | 171   | 0     | 0.47   |
| Samsung   | SSD 960 PRO        | 2 TB   | 1       | 170   | 0     | 0.47   |
| SK hynix  | BC511 NVMe         | 256 GB | 1       | 170   | 0     | 0.47   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 2       | 170   | 0     | 0.47   |
| Intel     | SSDPEDMW800G4      | 800 GB | 1       | 168   | 0     | 0.46   |
| Toshiba   | RD400              | 256 GB | 1       | 167   | 0     | 0.46   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 2       | 165   | 0     | 0.45   |
| ADATA     | SX8200PNP          | 512 GB | 4       | 164   | 0     | 0.45   |
| Kingston  | SKC2500M8500G      | 500 GB | 1       | 163   | 0     | 0.45   |
| PNY       | CS3030 500GB SSD   | 500 GB | 3       | 162   | 0     | 0.45   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 161   | 0     | 0.44   |
| SK hynix  | PC300 NVMe         | 256 GB | 1       | 159   | 0     | 0.44   |
| Intel     | SSDPEKNW512G8      | 512 GB | 5       | 159   | 0     | 0.44   |
| Corsair   | Force MP510        | 480 GB | 1       | 155   | 0     | 0.43   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 4       | 155   | 0     | 0.43   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 2       | 154   | 0     | 0.42   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 2       | 154   | 0     | 0.42   |
| Toshiba   | RC100              | 240 GB | 1       | 151   | 0     | 0.41   |
| ORICO     | V500               | 1 TB   | 1       | 149   | 0     | 0.41   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 2       | 147   | 0     | 0.40   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 7       | 180   | 1     | 0.40   |
| SK hynix  | BC501 NVMe         | 512 GB | 1       | 141   | 0     | 0.39   |
| Samsung   | SSD 970 EVO        | 1 TB   | 12      | 141   | 0     | 0.39   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 1       | 140   | 0     | 0.38   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 20      | 138   | 0     | 0.38   |
| ADATA     | IM2P33F8BR1-512GB  | 512 GB | 1       | 137   | 0     | 0.38   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 8       | 137   | 0     | 0.38   |
| LDLC      | F8+M.2 240         | 240 GB | 2       | 134   | 0     | 0.37   |
| Kingston  | SA1000M8480G       | 480 GB | 1       | 134   | 0     | 0.37   |
| Toshiba   | KBG40ZNS256G NVMe  | 256 GB | 1       | 133   | 0     | 0.37   |
| minisf... | 512GB              | 512 GB | 2       | 132   | 0     | 0.36   |
| Toshiba   | THNSF5256GCJ7      | 256 GB | 1       | 130   | 0     | 0.36   |
| Samsung   | PM991 NVMe         | 256 GB | 3       | 129   | 0     | 0.36   |
| ADATA     | SX8200NP           | 480 GB | 1       | 124   | 0     | 0.34   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 5       | 123   | 0     | 0.34   |
| SK hynix  | BC511 HFM256GDJ... | 256 GB | 4       | 123   | 0     | 0.34   |
| Seagate   | FireCuda 520 SS... | 500 GB | 5       | 122   | 0     | 0.34   |
| Corsair   | Force MP510        | 240 GB | 4       | 122   | 0     | 0.33   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 3       | 120   | 0     | 0.33   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 4       | 120   | 0     | 0.33   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 4       | 119   | 0     | 0.33   |
| Samsung   | SSD 960 PRO        | 512 GB | 3       | 213   | 2     | 0.32   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 19      | 117   | 0     | 0.32   |
| Kingston  | SA2000M8500G       | 500 GB | 8       | 116   | 0     | 0.32   |
| Samsung   | PM961 NVMe         | 512 GB | 1       | 116   | 0     | 0.32   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 1       | 115   | 0     | 0.32   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 2       | 115   | 0     | 0.32   |
| Micron    | 2300_MTFDHBA512TDV | 512 GB | 2       | 113   | 0     | 0.31   |
| Samsung   | MZVLB256HBHQ-000L2 | 256 GB | 1       | 112   | 0     | 0.31   |
| Samsung   | PM961 NVMe         | 256 GB | 1       | 112   | 0     | 0.31   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 1       | 111   | 0     | 0.30   |
| Kingston  | OM8PCP3512F-AI1    | 512 GB | 2       | 110   | 0     | 0.30   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 1       | 109   | 0     | 0.30   |
| Samsung   | PM981 NVMe         | 256 GB | 2       | 109   | 0     | 0.30   |
| Intel     | SSDPEKKW512G7      | 512 GB | 2       | 173   | 1     | 0.30   |
| HP        | SSD EX920          | 256 GB | 1       | 108   | 0     | 0.30   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 9       | 108   | 0     | 0.30   |
| ADATA     | SX8200PNP          | 256 GB | 5       | 105   | 0     | 0.29   |
| Kingston  | SA2000M8250G       | 250 GB | 9       | 104   | 0     | 0.29   |
| Corsair   | Force MP300        | 120 GB | 1       | 102   | 0     | 0.28   |
| Silico... | 512GB PCS PCIe ... | 512 GB | 1       | 99    | 0     | 0.27   |
| Kingston  | SA2000M81000G      | 1 TB   | 3       | 119   | 337   | 0.27   |
| Samsung   | MZVLW512HMJP-000H7 | 512 GB | 1       | 96    | 0     | 0.26   |
| ADATA     | SX6000LNP          | 128 GB | 1       | 96    | 0     | 0.26   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 9       | 92    | 0     | 0.25   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 1       | 91    | 0     | 0.25   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 6       | 91    | 0     | 0.25   |
| Corsair   | Force MP600        | 500 GB | 1       | 91    | 0     | 0.25   |
| Transcend | TS2TMTE220S        | 2 TB   | 2       | 90    | 0     | 0.25   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 1       | 89    | 0     | 0.25   |
| Silico... | M Series NVMe S... | 128 GB | 1       | 89    | 0     | 0.25   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 11      | 104   | 18    | 0.25   |
| Samsung   | SSD 970 EVO        | 500 GB | 17      | 89    | 0     | 0.25   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 1       | 89    | 0     | 0.24   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 2       | 89    | 0     | 0.24   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 4       | 85    | 0     | 0.23   |
| Gigabyte  | GP-AG42TB          | 2 TB   | 2       | 83    | 0     | 0.23   |
| WDC       | PC SN730 NVMe      | 1 TB   | 1       | 83    | 0     | 0.23   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 1       | 83    | 0     | 0.23   |
| KIOXIA    | KBG30ZMV256G       | 256 GB | 1       | 80    | 0     | 0.22   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 2       | 80    | 0     | 0.22   |
| HP        | SSD EX950          | 2 TB   | 1       | 79    | 0     | 0.22   |
| WDC       | WDS100T1X0E-00AFY0 | 1 TB   | 1       | 78    | 0     | 0.21   |
| Kingston  | OM8PCP3512F-AA     | 512 GB | 1       | 77    | 0     | 0.21   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 21      | 75    | 0     | 0.21   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 7       | 74    | 0     | 0.20   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 2       | 74    | 0     | 0.20   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 2       | 74    | 0     | 0.20   |
| Samsung   | MZVLW128HEGR-000L2 | 128 GB | 1       | 72    | 0     | 0.20   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 5       | 72    | 0     | 0.20   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 1       | 71    | 0     | 0.20   |
| SSSTC     | CL1-3D128-Q11 NVMe | 128 GB | 1       | 70    | 0     | 0.19   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 2       | 69    | 0     | 0.19   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 6       | 68    | 0     | 0.19   |
| Samsung   | MZVLW512HMJP-000L7 | 512 GB | 1       | 68    | 0     | 0.19   |
| HP        | SSD EX950          | 512 GB | 10      | 68    | 0     | 0.19   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 2       | 65    | 0     | 0.18   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 9       | 65    | 0     | 0.18   |
| Seagate   | IronWolf ZP500N... | 500 GB | 1       | 64    | 0     | 0.18   |
| Silico... | ASint AS806        | 128 GB | 1       | 63    | 0     | 0.18   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 4       | 58    | 0     | 0.16   |
| Silico... | NE-256             | 256 GB | 4       | 57    | 0     | 0.16   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 1       | 57    | 0     | 0.16   |
| Apple     | SSD SM0256L        | 256 GB | 1       | 57    | 0     | 0.16   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 3       | 56    | 0     | 0.15   |
| SK hynix  | PC611 NVMe         | 512 GB | 1       | 56    | 0     | 0.15   |
| SK hynix  | BC711 NVMe         | 256 GB | 1       | 55    | 0     | 0.15   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 1       | 55    | 0     | 0.15   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 1       | 55    | 0     | 0.15   |
| Samsung   | MZALQ512HALU-000L2 | 512 GB | 2       | 54    | 0     | 0.15   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 1       | 53    | 0     | 0.15   |
| Samsung   | SSD 970 PRO        | 1 TB   | 5       | 53    | 0     | 0.15   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 1       | 52    | 0     | 0.14   |
| Samsung   | MZVLB512HBJQ-000H1 | 512 GB | 1       | 51    | 0     | 0.14   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 3       | 49    | 0     | 0.14   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 2       | 49    | 0     | 0.14   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 1       | 49    | 0     | 0.14   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 1       | 48    | 0     | 0.13   |
| Union ... | UMIS LENSE40256... | 256 GB | 2       | 47    | 0     | 0.13   |
| Samsung   | MZVLB512HAJQ-000L2 | 512 GB | 1       | 44    | 0     | 0.12   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 3       | 44    | 0     | 0.12   |
| Samsung   | MZVLB2T0HMLB-00000 | 2 TB   | 1       | 41    | 0     | 0.11   |
| Samsung   | SSD 980            | 250 GB | 5       | 41    | 0     | 0.11   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 4       | 41    | 0     | 0.11   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 2       | 39    | 0     | 0.11   |
| Toshiba   | KBG40ZNT512G ME... | 512 GB | 1       | 39    | 0     | 0.11   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 2       | 39    | 0     | 0.11   |
| Micron    | 7300_MTFDHBA400TDG | 400 GB | 2       | 38    | 0     | 0.11   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 2       | 36    | 0     | 0.10   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 1       | 36    | 0     | 0.10   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 1       | 35    | 0     | 0.10   |
| Enmotus   | P200-1600-128      | 1.5 TB | 1       | 34    | 0     | 0.09   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 1       | 33    | 0     | 0.09   |
| Samsung   | SSD 960 EVO        | 1 TB   | 2       | 91    | 2     | 0.09   |
| Lite-On   | CA3-8D512          | 512 GB | 2       | 33    | 0     | 0.09   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 1       | 32    | 0     | 0.09   |
| Samsung   | SSD 980 PRO        | 250 GB | 4       | 32    | 0     | 0.09   |
| Crucial   | CT2000P5SSD8       | 2 TB   | 1       | 32    | 0     | 0.09   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 1       | 31    | 0     | 0.09   |
| Crucial   | CT500P5PSSD8       | 500 GB | 1       | 31    | 0     | 0.09   |
| Samsung   | MZVLB256HAHQ-000L2 | 256 GB | 1       | 30    | 0     | 0.08   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 1       | 30    | 0     | 0.08   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 29    | 0     | 0.08   |
| Seagate   | BarraCuda 510 S... | 512 GB | 1       | 29    | 0     | 0.08   |
| Gigabyte  | GP-GSM2NE3256GNTD  | 256 GB | 3       | 29    | 0     | 0.08   |
| Samsung   | MZVLQ256HAJD-000H1 | 256 GB | 2       | 29    | 0     | 0.08   |
| Phison    | minisforum         | 512 GB | 2       | 28    | 0     | 0.08   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 1       | 28    | 0     | 0.08   |
| WDC       | PC SN520 NVMe      | 256 GB | 1       | 28    | 0     | 0.08   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 2       | 28    | 0     | 0.08   |
| Samsung   | MZALQ128HBHQ-000L1 | 128 GB | 5       | 26    | 0     | 0.07   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 1       | 25    | 0     | 0.07   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 1       | 24    | 0     | 0.07   |
| Samsung   | MZVLQ512HALU-000H1 | 512 GB | 1       | 24    | 0     | 0.07   |
| Micron    | MTFDHBA512TCK      | 512 GB | 1       | 23    | 0     | 0.07   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 2       | 23    | 0     | 0.07   |
| ATP       | NVMe M.2 2280 SSD  | 240 GB | 2       | 23    | 0     | 0.06   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 2       | 22    | 0     | 0.06   |
| ADATA     | IM2P33F8BR2-512GB  | 512 GB | 1       | 22    | 0     | 0.06   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 5       | 22    | 0     | 0.06   |
| Colorful  | CN600              | 512 GB | 1       | 22    | 0     | 0.06   |
| SK hynix  | PC401 NVMe         | 256 GB | 1       | 22    | 0     | 0.06   |
| ADATA     | IM2P33F8BR2-256GB  | 256 GB | 1       | 22    | 0     | 0.06   |
| Samsung   | MZVL2512HCJQ-00B00 | 512 GB | 1       | 22    | 0     | 0.06   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 4       | 21    | 0     | 0.06   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 2       | 21    | 0     | 0.06   |
| SK hynix  | BC511 NVMe         | 512 GB | 2       | 21    | 0     | 0.06   |
| Goodram   | SSDPR-PX500-256-80 | 256 GB | 1       | 21    | 0     | 0.06   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 3       | 21    | 0     | 0.06   |
| V-GeN     | V-GEN06SM21AR51... | 512 GB | 1       | 21    | 0     | 0.06   |
| AGI       | AGI512G16AI198     | 512 GB | 1       | 63    | 2     | 0.06   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 2       | 20    | 0     | 0.05   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 2       | 18    | 0     | 0.05   |
| Gigabyte  | GP-GSM2NE3128GNTD  | 128 GB | 1       | 18    | 0     | 0.05   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 3       | 18    | 0     | 0.05   |
| KIOXIA    | KBG40ZNV1T02       | 1 TB   | 1       | 18    | 0     | 0.05   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 16    | 0     | 0.05   |
| WDC       | PC SN530 SDBPMP... | 512 GB | 1       | 15    | 0     | 0.04   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 1       | 15    | 0     | 0.04   |
| Samsung   | SSD 980            | 1 TB   | 4       | 15    | 0     | 0.04   |
| ADATA     | SX6000PNP          | 256 GB | 1       | 14    | 0     | 0.04   |
| Samsung   | MZVL2512HCJQ-00B07 | 512 GB | 4       | 14    | 0     | 0.04   |
| Toshiba   | KBG30ZPZ128G       | 128 GB | 1       | 14    | 0     | 0.04   |
| Phison    | Sabrent Rocket ... | 1 TB   | 1       | 14    | 0     | 0.04   |
| Samsung   | SSD 980 PRO        | 1 TB   | 4       | 14    | 0     | 0.04   |
| ADATA     | SX6000PNP          | 1 TB   | 1       | 13    | 0     | 0.04   |
| Micron    | 2200S NVMe         | 1 TB   | 2       | 13    | 0     | 0.04   |
| Kingston  | RBUSNS8154P3256GJ1 | 256 GB | 1       | 11    | 0     | 0.03   |
| Hikvision | HS-SSD-C2000ECO... | 1 TB   | 1       | 10    | 0     | 0.03   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 10    | 0     | 0.03   |
| SK hynix  | PC300 HFS512GD9... | 512 GB | 1       | 10    | 0     | 0.03   |
| Samsung   | PM981a NVMe        | 512 GB | 1       | 10    | 0     | 0.03   |
| Crucial   | CT250P2SSD8        | 250 GB | 4       | 10    | 0     | 0.03   |
| Toshiba   | KXG6APNV2T04       | 2 TB   | 1       | 10    | 0     | 0.03   |
| BIWIN     | SSD                | 1 TB   | 1       | 9     | 0     | 0.03   |
| WDC       | PC SN530 NVMe      | 512 GB | 1       | 9     | 0     | 0.02   |
| Mushkin   | MKNSSDHL500GB-D8   | 500 GB | 2       | 8     | 0     | 0.02   |
| Samsung   | PM9A1 NVMe         | 512 GB | 2       | 8     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 1       | 7     | 0     | 0.02   |
| Kingston  | SKC2500M8250G      | 250 GB | 1       | 7     | 0     | 0.02   |
| WDC       | PC SN530 NVMe      | 256 GB | 1       | 7     | 0     | 0.02   |
| FORESEE   | P900F128GBH        | 128 GB | 1       | 7     | 0     | 0.02   |
| Union ... | UMIS LENSE40512... | 512 GB | 1       | 6     | 0     | 0.02   |
| ADATA     | FALCON             | 256 GB | 1       | 6     | 0     | 0.02   |
| SK hynix  | SHGP31-500GM-2     | 500 GB | 3       | 6     | 0     | 0.02   |
| Kingston  | OM8PDP3512B-A01    | 512 GB | 5       | 6     | 0     | 0.02   |
| Silico... | Aura Pro X2        | 960 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | SSD 980 PRO        | 500 GB | 10      | 6     | 0     | 0.02   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 2       | 6     | 0     | 0.02   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 3       | 6     | 0     | 0.02   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | SSD 980            | 500 GB | 4       | 5     | 0     | 0.02   |
| Toshiba   | KBG30ZMV256G KI... | 256 GB | 1       | 5     | 0     | 0.01   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 2       | 5     | 0     | 0.01   |
| Crucial   | CT500P5SSD8        | 500 GB | 3       | 5     | 0     | 0.01   |
| Crucial   | CT500P2SSD8        | 500 GB | 4       | 5     | 0     | 0.01   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 1       | 5     | 0     | 0.01   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 1       | 4     | 0     | 0.01   |
| HP        | SSD EX900          | 500 GB | 1       | 4     | 0     | 0.01   |
| WDC       | WDS500G1X0E-00AFY0 | 500 GB | 3       | 4     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 1       | 3     | 0     | 0.01   |
| SK hynix  | HFM256GDHTNG-8510B | 256 GB | 1       | 3     | 0     | 0.01   |
| SanDisk   | Ultra 3D NVMe      | 500 GB | 1       | 3     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 2       | 2     | 0     | 0.01   |
| Phison    | APS-SE20G-256      | 256 GB | 1       | 2     | 0     | 0.01   |
| T-FORCE   | TM8FP7001T         | 1 TB   | 1       | 2     | 0     | 0.01   |
| Micron    | MTFDHBA512TDV      | 512 GB | 1       | 2     | 0     | 0.01   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 1       | 2     | 0     | 0.01   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 2       | 2     | 0     | 0.01   |
| Kingston  | OM8PDP3256B-A01    | 256 GB | 3       | 2     | 0     | 0.01   |
| Samsung   | SSD 980 PRO        | 2 TB   | 2       | 2     | 0     | 0.01   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MZALQ256HAJD-000L2 | 256 GB | 1       | 2     | 0     | 0.01   |
| Micron    | 2450_MTFDKBA1T0TFK | 1 TB   | 1       | 2     | 0     | 0.01   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 1       | 1     | 0     | 0.01   |
| Samsung   | MZVL21T0HCLR-00BL7 | 1 TB   | 2       | 1     | 0     | 0.01   |
| Transcend | TS256GMTE652T2     | 256 GB | 2       | 1     | 0     | 0.00   |
| Union ... | RPFTJ128PDD2EWX    | 128 GB | 1       | 1     | 0     | 0.00   |
| Pioneer   | APS-SE10N-256      | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 1       | 1     | 0     | 0.00   |
| Seagate   | FireCuda 510 SS... | 500 GB | 1       | 1     | 0     | 0.00   |
| Kingston  | OM8SBP3512K-AH     | 512 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | PM981 NVMe         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Micron    | 2200S NVMe         | 512 GB | 1       | 1     | 0     | 0.00   |
| Lexar     | 250GB SSD          | 250 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD_BLACK SN850     | 1 TB   | 1       | 0     | 0     | 0.00   |
| Kingston  | OM8PCP3512F-A02    | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | PC611 NVMe         | 256 GB | 1       | 0     | 0     | 0.00   |
| Micron    | 3400_MTFDKBA1T0TFH | 1 TB   | 1       | 0     | 0     | 0.00   |
| LDLC      | F8+M.2 480         | 480 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZALQ512HBLU-00BL1 | 512 GB | 4       | 0     | 0     | 0.00   |
| Solid ... | CL1-3D128-Q11 N... | 128 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | KXG60PNV2T04 NV... | 2 TB   | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 2       | 0     | 0     | 0.00   |
| SK hynix  | HFM512GDHTNG-8310A | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLB512HBJQ-000   | 512 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 1       | 0     | 0     | 0.00   |
| Seagate   | BarraCuda 510 S... | 250 GB | 1       | 0     | 0     | 0.00   |
| EMTEC     | X300               | 128 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVL2256HCHQ-00B00 | 256 GB | 1       | 0     | 0     | 0.00   |
| ShiJi     | 256GB M.2-NVMe     | 256 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | SX6000LNP          | 512 GB | 2       | 0     | 0     | 0.00   |
| Kingston  | SEDC1000BM8240G    | 240 GB | 1       | 0     | 0     | 0.00   |
| Silico... | 500GB-PRO-X-SS     | 500 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SHGP31-1000GM      | 1 TB   | 1       | 0     | 0     | 0.00   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| Plextor     | 2      | 2       | 908   | 0     | 2.49   |
| Patriot     | 1      | 1       | 493   | 0     | 1.35   |
| Intel       | 26     | 59      | 246   | 1     | 0.67   |
| SPCC        | 4      | 8       | 216   | 0     | 0.59   |
| Transcend   | 5      | 9       | 205   | 0     | 0.56   |
| Lenovo      | 2      | 2       | 202   | 0     | 0.56   |
| PNY         | 2      | 6       | 181   | 0     | 0.50   |
| HP          | 6      | 16      | 167   | 0     | 0.46   |
| ADATA       | 14     | 30      | 163   | 0     | 0.45   |
| Corsair     | 6      | 10      | 162   | 0     | 0.44   |
| KIOXIA      | 7      | 11      | 160   | 0     | 0.44   |
| Phison      | 10     | 31      | 157   | 0     | 0.43   |
| Toshiba     | 24     | 29      | 155   | 0     | 0.43   |
| ORICO       | 1      | 1       | 149   | 0     | 0.41   |
| Samsung     | 87     | 315     | 145   | 1     | 0.39   |
| minisforum  | 1      | 2       | 132   | 0     | 0.36   |
| WDC         | 47     | 97      | 118   | 0     | 0.33   |
| Kingston    | 20     | 46      | 98    | 22    | 0.27   |
| LDLC        | 2      | 3       | 90    | 0     | 0.25   |
| Silicon ... | 8      | 11      | 84    | 0     | 0.23   |
| Seagate     | 7      | 11      | 77    | 0     | 0.21   |
| Crucial     | 9      | 37      | 77    | 6     | 0.20   |
| Mushkin     | 2      | 3       | 71    | 0     | 0.20   |
| Apple       | 1      | 1       | 57    | 0     | 0.16   |
| Micron      | 11     | 15      | 52    | 0     | 0.14   |
| SK hynix    | 24     | 40      | 49    | 0     | 0.13   |
| SSSTC       | 2      | 3       | 42    | 0     | 0.12   |
| Gigabyte    | 5      | 9       | 41    | 0     | 0.11   |
| XPG         | 1      | 4       | 41    | 0     | 0.11   |
| Enmotus     | 1      | 1       | 34    | 0     | 0.09   |
| Lite-On     | 1      | 2       | 33    | 0     | 0.09   |
| Union Me... | 3      | 4       | 25    | 0     | 0.07   |
| ATP         | 1      | 2       | 23    | 0     | 0.06   |
| Colorful    | 1      | 1       | 22    | 0     | 0.06   |
| Goodram     | 1      | 1       | 21    | 0     | 0.06   |
| V-GeN       | 1      | 1       | 21    | 0     | 0.06   |
| AGI         | 1      | 1       | 63    | 2     | 0.06   |
| Hikvision   | 1      | 1       | 10    | 0     | 0.03   |
| BIWIN       | 1      | 1       | 9     | 0     | 0.03   |
| FORESEE     | 1      | 1       | 7     | 0     | 0.02   |
| T-FORCE     | 1      | 1       | 2     | 0     | 0.01   |
| SanDisk     | 2      | 2       | 2     | 0     | 0.01   |
| Pioneer     | 1      | 1       | 1     | 0     | 0.00   |
| Lexar       | 1      | 1       | 0     | 0     | 0.00   |
| Solid St... | 1      | 1       | 0     | 0     | 0.00   |
| EMTEC       | 1      | 1       | 0     | 0     | 0.00   |
| ShiJi       | 1      | 1       | 0     | 0     | 0.00   |

