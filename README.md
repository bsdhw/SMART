HDD/SSD Reliability Test
========================

This is a project to estimate reliability of HDD/SSD drives by
the analysis of SMART data collected by BSD users at https://bsd-hardware.info. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe/blob/master/INSTALL.BSD.md) tool:

    hw-probe -all -upload

Total drives: 4826.

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

See complete list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Seagate   | ST3120023A         | 120 GB | 1       | 5214  | 0     | 14.29  |
| Samsung   | HD502IJ            | 500 GB | 1       | 4726  | 0     | 12.95  |
| WDC       | WD800JD-08MSA1     | 80 GB  | 1       | 4687  | 0     | 12.84  |
| WDC       | WD1600AAJS-00PSA0  | 160 GB | 1       | 4208  | 0     | 11.53  |
| WDC       | WD1600JB-00REA0    | 160 GB | 1       | 4140  | 0     | 11.34  |
| WDC       | WD1600JD-00GBB0    | 160 GB | 4       | 5313  | 4     | 11.14  |
| WDC       | WD1602ABJS-43P5A0  | 160 GB | 1       | 4045  | 0     | 11.08  |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 3       | 3833  | 0     | 10.50  |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 1       | 3820  | 0     | 10.47  |
| Hitachi   | HDT721010SLA360    | 1 TB   | 1       | 3782  | 0     | 10.36  |
| Hitachi   | HDS725050KLA360    | 500 GB | 1       | 3763  | 0     | 10.31  |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 2       | 3704  | 0     | 10.15  |
| Hitachi   | HDT721032SLA360    | 320 GB | 1       | 3534  | 0     | 9.68   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 4       | 3472  | 0     | 9.51   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 3       | 3329  | 0     | 9.12   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 6       | 3085  | 0     | 8.45   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 4       | 3039  | 0     | 8.33   |
| WDC       | WD1602ABKS-18N8A0  | 160 GB | 1       | 2978  | 0     | 8.16   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 3       | 2977  | 0     | 8.16   |
| WDC       | WD800EB-00DJF0     | 80 GB  | 1       | 2959  | 0     | 8.11   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 1       | 2917  | 0     | 7.99   |
| WDC       | WD400BB-00GFA0     | 40 GB  | 1       | 2808  | 0     | 7.69   |
| Hitachi   | HUA7250SBSUN500G   | 500 GB | 2       | 2785  | 0     | 7.63   |
| Seagate   | ST3500630NS        | 500 GB | 3       | 2715  | 0     | 7.44   |
| Seagate   | ST32000645NS       | 2 TB   | 1       | 2713  | 0     | 7.43   |
| Hitachi   | HDT725025VLA380    | 250 GB | 1       | 2680  | 0     | 7.34   |
| WDC       | WD3200AAKX-00ERMA0 | 320 GB | 1       | 2660  | 0     | 7.29   |
| Seagate   | ST33000651NS       | 3 TB   | 1       | 2619  | 0     | 7.18   |
| Hitachi   | HUA721050KLA330    | 500 GB | 2       | 3842  | 1     | 7.02   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 1       | 2510  | 0     | 6.88   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 1       | 2483  | 0     | 6.81   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 1       | 2444  | 0     | 6.70   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 3       | 2436  | 0     | 6.67   |
| WDC       | WD1600AABS-61PRA0  | 160 GB | 1       | 2420  | 0     | 6.63   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 1       | 2414  | 0     | 6.61   |
| HP        | GB0250EAFYK        | 250 GB | 3       | 3054  | 1     | 6.61   |
| Samsung   | HD103SJ            | 1 TB   | 4       | 2821  | 1     | 6.60   |
| Maxtor    | 6V080E0            | 82 GB  | 1       | 2371  | 0     | 6.50   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 2       | 2344  | 0     | 6.42   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 1       | 2343  | 0     | 6.42   |
| WDC       | WD1003FBYX-23 0... | 1 TB   | 2       | 2317  | 0     | 6.35   |
| Seagate   | ST380011A          | 80 GB  | 2       | 2314  | 0     | 6.34   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 3       | 2281  | 0     | 6.25   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 1       | 2257  | 0     | 6.19   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 4       | 2235  | 0     | 6.12   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 1       | 2233  | 0     | 6.12   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 1       | 2187  | 0     | 5.99   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 1       | 2183  | 0     | 5.98   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 2168  | 0     | 5.94   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 5       | 2150  | 0     | 5.89   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 12      | 2406  | 1     | 5.82   |
| Hitachi   | HDS728080PLA380    | 82 GB  | 1       | 2086  | 0     | 5.72   |
| Hitachi   | HDS5C4040ALE630    | 4 TB   | 21      | 2076  | 0     | 5.69   |
| Seagate   | ST32000641AS       | 2 TB   | 1       | 2076  | 0     | 5.69   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 1       | 2053  | 0     | 5.63   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 4       | 2053  | 0     | 5.62   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 1       | 2024  | 0     | 5.55   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 3       | 1988  | 0     | 5.45   |
| HGST      | HUS724020ALA640    | 2 TB   | 6       | 1955  | 0     | 5.36   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 2       | 1944  | 0     | 5.33   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 5       | 2167  | 1     | 5.27   |
| HGST      | HTE725032A7E630    | 320 GB | 1       | 1922  | 0     | 5.27   |
| Seagate   | ST3320620A         | 320 GB | 1       | 1913  | 0     | 5.24   |
| WDC       | WD360ADFD-00NLR5   | 37 GB  | 1       | 1910  | 0     | 5.23   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 18      | 2020  | 2     | 5.23   |
| Samsung   | HD204UI            | 2 TB   | 14      | 2533  | 8     | 5.22   |
| Seagate   | ST3160215ACE       | 160 GB | 1       | 1863  | 0     | 5.11   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 1       | 1848  | 0     | 5.06   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 3       | 2230  | 1     | 5.06   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 6       | 2134  | 2     | 5.04   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 1       | 1827  | 0     | 5.01   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 1       | 1824  | 0     | 5.00   |
| HGST      | HUH728060ALE600    | 6 TB   | 1       | 1820  | 0     | 4.99   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 1       | 1819  | 0     | 4.98   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 2       | 1816  | 0     | 4.98   |
| Hitachi   | HTE545050B9A300    | 500 GB | 1       | 1809  | 0     | 4.96   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 11      | 1929  | 184   | 4.95   |
| Maxtor    | STM3250820A        | 250 GB | 1       | 1802  | 0     | 4.94   |
| Seagate   | ST9320421AS        | 320 GB | 1       | 1802  | 0     | 4.94   |
| Hitachi   | HTS545016B9A300    | 160 GB | 1       | 1788  | 0     | 4.90   |
| Hitachi   | HTS727550A9E364    | 500 GB | 2       | 1757  | 0     | 4.82   |
| Samsung   | HD501LJ            | 500 GB | 6       | 3070  | 2     | 4.77   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 2       | 1670  | 0     | 4.58   |
| HGST      | HDN724040ALE640    | 4 TB   | 17      | 1920  | 48    | 4.57   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 2       | 1654  | 0     | 4.53   |
| Samsung   | HD502HJ            | 500 GB | 3       | 2221  | 1     | 4.53   |
| WDC       | WD5000BEVT-00A03T0 | 500 GB | 1       | 1643  | 0     | 4.50   |
| Toshiba   | MG03ACA200         | 2 TB   | 5       | 1631  | 0     | 4.47   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 12      | 1910  | 169   | 4.36   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 4       | 1574  | 0     | 4.31   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 1       | 1566  | 0     | 4.29   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 9       | 1549  | 0     | 4.25   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 4       | 1546  | 0     | 4.24   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 1       | 1543  | 0     | 4.23   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 1       | 1542  | 0     | 4.23   |
| Toshiba   | MG04ACA400E        | 4 TB   | 2       | 1535  | 0     | 4.21   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 4       | 1527  | 0     | 4.19   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 1       | 1522  | 0     | 4.17   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 2       | 1518  | 0     | 4.16   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 2       | 1517  | 0     | 4.16   |
| Maxtor    | 6L080J4            | 80 GB  | 3       | 2093  | 2     | 4.15   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 3       | 1514  | 0     | 4.15   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 2       | 1504  | 0     | 4.12   |
| WDC       | WD7500BMVW-11AJGS4 | 752 GB | 1       | 1500  | 0     | 4.11   |
| Seagate   | ST3500412AS        | 500 GB | 1       | 1499  | 0     | 4.11   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 3       | 3419  | 4     | 4.09   |
| HP        | MB1000GCWCV        | 1 TB   | 7       | 1962  | 4     | 4.08   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 3       | 3153  | 4     | 4.05   |
| Seagate   | ST8000DM002-1YW112 | 8 TB   | 1       | 1475  | 0     | 4.04   |
| WDC       | WD2000FYYX         | 2 TB   | 4       | 1466  | 0     | 4.02   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 2       | 1449  | 0     | 3.97   |
| WDC       | WD10PURX-64D85Y0   | 1 TB   | 1       | 1445  | 0     | 3.96   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 10      | 1794  | 124   | 3.96   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 3       | 1529  | 3     | 3.92   |
| Hitachi   | HDS721075KLA330    | 752 GB | 9       | 1767  | 1     | 3.90   |
| Toshiba   | MD04ACA500         | 5 TB   | 1       | 1413  | 0     | 3.87   |
| Seagate   | ST3750528AS        | 752 GB | 2       | 1401  | 0     | 3.84   |
| Seagate   | ST9250410AS        | 250 GB | 1       | 1400  | 0     | 3.84   |
| WDC       | WD5002ABYS-18B1B0  | 500 GB | 2       | 2250  | 4     | 3.82   |
| WDC       | WD2500AAJS-00L7A0  | 250 GB | 1       | 1391  | 0     | 3.81   |
| HGST      | HDN724030ALE640    | 3 TB   | 3       | 1389  | 0     | 3.81   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 19      | 1694  | 2     | 3.78   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 1       | 1376  | 0     | 3.77   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 4       | 1797  | 28    | 3.71   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 3       | 2182  | 874   | 3.68   |
| Seagate   | ST6000DM001-1YW11C | 6 TB   | 1       | 1338  | 0     | 3.67   |
| Hitachi   | HDS721032CLA362    | 320 GB | 1       | 1323  | 0     | 3.63   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 1       | 1323  | 0     | 3.63   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 6       | 1729  | 63    | 3.61   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 1       | 1317  | 0     | 3.61   |
| WDC       | WD5000BMVV-11A1CS0 | 500 GB | 1       | 1308  | 0     | 3.59   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 49      | 1542  | 2     | 3.58   |
| Toshiba   | DT01ACA200         | 2 TB   | 5       | 1304  | 0     | 3.57   |
| WDC       | WD1600BEVS-75RST0  | 160 GB | 1       | 1301  | 0     | 3.57   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 14      | 1460  | 1     | 3.55   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 5       | 1296  | 0     | 3.55   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 1       | 1296  | 0     | 3.55   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 1       | 1289  | 0     | 3.53   |
| WDC       | WD5003ABYX-88 LEN  | 500 GB | 1       | 1280  | 0     | 3.51   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 2       | 1268  | 0     | 3.48   |
| Samsung   | HD502HI            | 500 GB | 2       | 1266  | 0     | 3.47   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 1       | 1266  | 0     | 3.47   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 4       | 1258  | 0     | 3.45   |
| Samsung   | HD322HJ            | 320 GB | 2       | 1257  | 0     | 3.44   |
| Seagate   | ST3160318AS        | 160 GB | 3       | 1244  | 0     | 3.41   |
| HGST      | HUS726040ALN610    | 4 TB   | 2       | 1239  | 0     | 3.40   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 2       | 1237  | 0     | 3.39   |
| Samsung   | HM500JI            | 500 GB | 3       | 1578  | 70    | 3.37   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 1       | 3656  | 2     | 3.34   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 1       | 3610  | 2     | 3.30   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 18      | 1301  | 58    | 3.29   |
| HP        | FB160C4081         | 160 GB | 3       | 3161  | 3     | 3.27   |
| WDC       | WD3750LMCW-11D9GS3 | 375 GB | 1       | 1179  | 0     | 3.23   |
| Samsung   | HD753LJ            | 752 GB | 3       | 1770  | 48    | 3.19   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 1       | 1158  | 0     | 3.17   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 2       | 1158  | 0     | 3.17   |
| Samsung   | SP2504C            | 250 GB | 1       | 1158  | 0     | 3.17   |
| Toshiba   | DT01ACA300         | 3 TB   | 9       | 1429  | 115   | 3.17   |
| Seagate   | ST3250312AS        | 250 GB | 4       | 1153  | 0     | 3.16   |
| HGST      | HDN728080ALE604    | 8 TB   | 7       | 1152  | 0     | 3.16   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 1       | 1146  | 0     | 3.14   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 10      | 1146  | 0     | 3.14   |
| WDC       | WD3000BLFS-60YBU2  | 304 GB | 2       | 1399  | 1     | 3.13   |
| Seagate   | ST3250318AS        | 250 GB | 4       | 1260  | 36    | 3.11   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 4       | 1463  | 164   | 3.09   |
| Hitachi   | HDS5C1050CLA382    | 500 GB | 1       | 1122  | 0     | 3.08   |
| Seagate   | ST500DM009-2DM14C  | 500 GB | 1       | 1122  | 0     | 3.08   |
| Samsung   | HD103UJ            | 1 TB   | 8       | 1833  | 30    | 3.01   |
| WDC       | WD360GD-00FLC0     | 37 GB  | 1       | 1099  | 0     | 3.01   |
| Toshiba   | MG03ACA100         | 1 TB   | 6       | 1096  | 0     | 3.00   |
| WDC       | WD5000BEKT-22KA9T0 | 500 GB | 1       | 1085  | 0     | 2.97   |
| Seagate   | ST320VT000-1BS14C  | 320 GB | 1       | 1083  | 0     | 2.97   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 5       | 1429  | 203   | 2.94   |
| Toshiba   | MQ01UBB200         | 2 TB   | 1       | 1067  | 0     | 2.93   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 13      | 1142  | 1     | 2.91   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 11      | 1060  | 0     | 2.91   |
| HGST      | HUS724040ALA640    | 4 TB   | 5       | 1058  | 0     | 2.90   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 1       | 1057  | 0     | 2.90   |
| Seagate   | ST3160023A         | 160 GB | 1       | 1056  | 0     | 2.89   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 3       | 1273  | 1     | 2.88   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 1       | 1051  | 0     | 2.88   |
| Toshiba   | MQ01ABD100H        | 1 TB   | 2       | 1041  | 0     | 2.85   |
| WDC       | WD2000JB-00FUA0    | 200 GB | 1       | 1023  | 0     | 2.81   |
| Toshiba   | MC04ACA400E        | 4 TB   | 2       | 1023  | 0     | 2.80   |
| Seagate   | ST32000542AS       | 2 TB   | 2       | 1508  | 482   | 2.80   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 2       | 1018  | 0     | 2.79   |
| ExcelStor | J8160              | 164 GB | 2       | 1015  | 0     | 2.78   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 1       | 1014  | 0     | 2.78   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 1       | 1007  | 0     | 2.76   |
| Seagate   | ST33000651AS       | 3 TB   | 2       | 1003  | 0     | 2.75   |
| Seagate   | ST3500413AS        | 500 GB | 11      | 1346  | 93    | 2.75   |
| Toshiba   | HDWE150            | 5 TB   | 6       | 1186  | 5     | 2.73   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 1       | 991   | 0     | 2.72   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 4       | 1370  | 2     | 2.69   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 1449  | 1     | 2.65   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 3       | 965   | 0     | 2.65   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 7       | 1390  | 11    | 2.63   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 3       | 960   | 0     | 2.63   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 2       | 960   | 0     | 2.63   |
| Samsung   | HD203WI            | 2 TB   | 1       | 959   | 0     | 2.63   |
| Toshiba   | MQ01ABB200         | 2 TB   | 1       | 953   | 0     | 2.61   |
| Seagate   | ST3000DM003-2AE16L | 3 TB   | 1       | 947   | 0     | 2.60   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 4       | 1105  | 2     | 2.59   |
| Seagate   | ST31000524AS       | 1 TB   | 6       | 1137  | 4     | 2.58   |
| WDC       | WD3200BEVS-08VAT2  | 320 GB | 1       | 936   | 0     | 2.57   |
| CLOVER    | CD253GJ            | 250 GB | 1       | 928   | 0     | 2.54   |
| Hitachi   | HTS545025B9A300    | 250 GB | 2       | 922   | 0     | 2.53   |
| Seagate   | ST1000NM0011       | 1 TB   | 3       | 1743  | 11    | 2.52   |
| Samsung   | HD321HJ            | 320 GB | 1       | 914   | 0     | 2.51   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 1       | 910   | 0     | 2.49   |
| WDC       | WD7500BPKT-22PK4T0 | 752 GB | 1       | 910   | 0     | 2.49   |
| Toshiba   | MQ04UBD200         | 2 TB   | 1       | 906   | 0     | 2.48   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 2       | 905   | 0     | 2.48   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 6       | 1575  | 3     | 2.48   |
| HGST      | HDN721010ALE604    | 10 TB  | 3       | 904   | 0     | 2.48   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1316  | 6     | 2.47   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 2       | 892   | 0     | 2.44   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 2       | 890   | 0     | 2.44   |
| WDC       | WD2500JS-75NCB2    | 250 GB | 2       | 889   | 0     | 2.44   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 1       | 888   | 0     | 2.43   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 5       | 887   | 0     | 2.43   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 3       | 1105  | 400   | 2.42   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 1       | 882   | 0     | 2.42   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 25      | 1131  | 55    | 2.41   |
| WDC       | WD1600AAJS-60B4A0  | 160 GB | 1       | 872   | 0     | 2.39   |
| Samsung   | HD154UI            | 1.5 TB | 4       | 1849  | 38    | 2.38   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 14      | 1029  | 83    | 2.37   |
| Seagate   | ST320410A          | 20 GB  | 1       | 2579  | 2     | 2.36   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 1       | 856   | 0     | 2.35   |
| WDC       | WD2500BEVT-00A23T0 | 250 GB | 1       | 851   | 0     | 2.33   |
| WDC       | WD80PURZ-85YNPY0   | 8 TB   | 1       | 851   | 0     | 2.33   |
| Seagate   | ST91000640NS       | 1 TB   | 2       | 847   | 0     | 2.32   |
| Seagate   | ST380815AS         | 80 GB  | 3       | 923   | 337   | 2.31   |
| Seagate   | ST3500312CS        | 500 GB | 7       | 840   | 0     | 2.30   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 7       | 961   | 2     | 2.29   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 1       | 828   | 0     | 2.27   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 1       | 2471  | 2     | 2.26   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 7       | 823   | 0     | 2.26   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 3       | 822   | 0     | 2.25   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 3       | 1049  | 3     | 2.25   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 1       | 819   | 0     | 2.25   |
| WDC       | WD1200BB-00HTA0    | 120 GB | 2       | 1633  | 347   | 2.24   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 1       | 816   | 0     | 2.24   |
| WDC       | WD2500JS-58NCB1    | 250 GB | 1       | 805   | 0     | 2.21   |
| Toshiba   | MK4032GAX          | 40 GB  | 1       | 802   | 0     | 2.20   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 2       | 802   | 0     | 2.20   |
| Lenovo    | WD2004FBYZ-23YC... | 2 TB   | 4       | 802   | 0     | 2.20   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 1       | 799   | 0     | 2.19   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 10      | 851   | 4     | 2.18   |
| WDC       | WD10JQLX-22JFGT0   | 1 TB   | 1       | 790   | 0     | 2.17   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 1       | 790   | 0     | 2.17   |
| Maxtor    | STM3250310AS       | 250 GB | 2       | 786   | 0     | 2.16   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 2       | 786   | 0     | 2.15   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 1       | 786   | 0     | 2.15   |
| WDC       | WD2500BEKT-75PVMT0 | 250 GB | 1       | 782   | 0     | 2.14   |
| WDC       | WD5000BPKT-60PK4T0 | 500 GB | 1       | 781   | 0     | 2.14   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 2       | 1318  | 4     | 2.12   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 1       | 769   | 0     | 2.11   |
| WDC       | WD15EARS-00Z5B1    | 1.5 TB | 1       | 3841  | 4     | 2.11   |
| Seagate   | ST3250310AS        | 250 GB | 2       | 1423  | 1     | 2.10   |
| Seagate   | ST380817AS         | 80 GB  | 4       | 760   | 0     | 2.08   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 2       | 754   | 0     | 2.07   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 1       | 751   | 0     | 2.06   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 9       | 1381  | 248   | 2.04   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 5       | 899   | 1     | 2.04   |
| Samsung   | HD103SI            | 1 TB   | 4       | 900   | 757   | 2.03   |
| Seagate   | ST96812AS          | 64 GB  | 1       | 741   | 0     | 2.03   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 2       | 739   | 0     | 2.02   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 1       | 734   | 0     | 2.01   |
| Toshiba   | DT01ACA100         | 1 TB   | 21      | 733   | 0     | 2.01   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 6       | 733   | 0     | 2.01   |
| Toshiba   | MD04ACA400         | 4 TB   | 1       | 732   | 0     | 2.01   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 4       | 731   | 0     | 2.00   |
| WDC       | WD1002FBYS-50A6B1  | 1 TB   | 1       | 727   | 0     | 1.99   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 1       | 725   | 0     | 1.99   |
| Seagate   | ST31000424CS       | 1 TB   | 1       | 721   | 0     | 1.98   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 1       | 720   | 0     | 1.97   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 9       | 1145  | 207   | 1.97   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 1       | 710   | 0     | 1.95   |
| Toshiba   | DT01ACA050         | 500 GB | 7       | 952   | 28    | 1.95   |
| WDC       | WD5000LPVT-75G33T0 | 500 GB | 1       | 708   | 0     | 1.94   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 1       | 707   | 0     | 1.94   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 2       | 706   | 0     | 1.93   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 3       | 705   | 0     | 1.93   |
| HGST      | HUS722T2TALA600    | 2 TB   | 1       | 700   | 0     | 1.92   |
| Toshiba   | MK2561GSY          | 250 GB | 1       | 695   | 0     | 1.91   |
| Seagate   | ST2000NM0011       | 2 TB   | 1       | 2080  | 2     | 1.90   |
| Toshiba   | MK1002TSKB         | 1 TB   | 1       | 692   | 0     | 1.90   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 11      | 692   | 0     | 1.90   |
| Seagate   | ST3320418AS        | 320 GB | 4       | 886   | 273   | 1.90   |
| Seagate   | ST3320620NS        | 320 GB | 1       | 2076  | 2     | 1.90   |
| Hitachi   | HDP725025GLA380    | 250 GB | 2       | 938   | 2     | 1.89   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 3       | 687   | 0     | 1.88   |
| Seagate   | ST2000NM0018-2F... | 2 TB   | 1       | 684   | 0     | 1.88   |
| WDC       | WD10JPVX-35JC3T0   | 1 TB   | 1       | 682   | 0     | 1.87   |
| MaxDig... | MD4000GSA6472E     | 4 TB   | 1       | 681   | 0     | 1.87   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 1       | 678   | 0     | 1.86   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 2       | 674   | 0     | 1.85   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 3       | 666   | 0     | 1.83   |
| HGST      | HDN726040ALE614    | 4 TB   | 2       | 661   | 0     | 1.81   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 3       | 885   | 1     | 1.77   |
| Hitachi   | HTS723225L9A360    | 250 GB | 1       | 644   | 0     | 1.77   |
| WDC       | WD7500BPKX-75HPJT0 | 752 GB | 1       | 642   | 0     | 1.76   |
| Fujitsu   | MHW2120BH          | 120 GB | 1       | 641   | 0     | 1.76   |
| Seagate   | ST3320820AS        | 320 GB | 1       | 635   | 0     | 1.74   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 1       | 633   | 0     | 1.74   |
| Seagate   | ST3320620AS        | 320 GB | 3       | 736   | 57    | 1.74   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 1       | 625   | 0     | 1.71   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 2       | 620   | 0     | 1.70   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 615   | 0     | 1.69   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 2       | 615   | 0     | 1.69   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 1       | 614   | 0     | 1.68   |
| WDC       | WD2500AAKX-19U6AA0 | 250 GB | 1       | 613   | 0     | 1.68   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 59      | 616   | 1     | 1.67   |
| WDC       | WD2500LPCX-24C6HT0 | 250 GB | 1       | 608   | 0     | 1.67   |
| WDC       | WD2500AAJS-40RYA0  | 250 GB | 1       | 603   | 0     | 1.65   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 4       | 793   | 416   | 1.63   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 1       | 596   | 0     | 1.63   |
| Toshiba   | MQ04UBF100         | 1 TB   | 1       | 592   | 0     | 1.62   |
| WDC       | WD2000JB-00GVC0    | 200 GB | 1       | 3539  | 5     | 1.62   |
| Seagate   | ST380013AS         | 80 GB  | 2       | 1985  | 4     | 1.58   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 2       | 575   | 0     | 1.58   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 5       | 574   | 0     | 1.57   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 3       | 1410  | 2     | 1.57   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 3       | 573   | 0     | 1.57   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 4       | 571   | 0     | 1.57   |
| HGST      | HTS721010A9E630    | 1 TB   | 13      | 589   | 79    | 1.56   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 5       | 569   | 0     | 1.56   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 2       | 568   | 0     | 1.56   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 8       | 564   | 0     | 1.55   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 8       | 557   | 0     | 1.53   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 2       | 549   | 0     | 1.50   |
| Samsung   | HD160JJ-P          | 160 GB | 1       | 547   | 0     | 1.50   |
| Hitachi   | HTS725050A7E630    | 500 GB | 1       | 535   | 0     | 1.47   |
| WDC       | WD3200AAKS-00V6A0  | 320 GB | 1       | 533   | 0     | 1.46   |
| WDC       | WD3200BEKT-60PVMT0 | 320 GB | 1       | 530   | 0     | 1.45   |
| IBM       | DBCA-204860        | 4 GB   | 1       | 522   | 0     | 1.43   |
| Seagate   | ST9160310AS        | 160 GB | 1       | 2600  | 4     | 1.43   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 1       | 517   | 0     | 1.42   |
| WDC       | WD5000AAKX-08ANVA0 | 500 GB | 1       | 516   | 0     | 1.42   |
| Seagate   | ST3160812AS        | 160 GB | 2       | 516   | 0     | 1.41   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 1       | 516   | 0     | 1.41   |
| Toshiba   | HDWN180            | 8 TB   | 8       | 513   | 0     | 1.41   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 1       | 512   | 0     | 1.40   |
| Seagate   | ST3500418AS        | 500 GB | 12      | 1240  | 65    | 1.40   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 1       | 508   | 0     | 1.39   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 2       | 507   | 0     | 1.39   |
| WDC       | WD400BD-75LRA0     | 40 GB  | 1       | 503   | 0     | 1.38   |
| Hitachi   | HDS721616PLA380    | 160 GB | 1       | 500   | 0     | 1.37   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 14      | 687   | 3     | 1.37   |
| Samsung   | HD161HJ            | 160 GB | 3       | 498   | 0     | 1.37   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 6       | 494   | 0     | 1.36   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 15      | 543   | 1     | 1.33   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 14      | 564   | 1     | 1.32   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 1       | 479   | 0     | 1.31   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 4       | 762   | 2     | 1.31   |
| HGST      | HTS541010A9E680    | 1 TB   | 8       | 475   | 255   | 1.29   |
| Seagate   | ST6000NE0023-2E... | 6 TB   | 2       | 840   | 4     | 1.28   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 3       | 1490  | 3     | 1.27   |
| HGST      | HTS725032A7E630    | 320 GB | 1       | 464   | 0     | 1.27   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 6       | 460   | 0     | 1.26   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 25      | 915   | 369   | 1.26   |
| Fujitsu   | MHY2120BH          | 120 GB | 2       | 456   | 0     | 1.25   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 1       | 455   | 0     | 1.25   |
| Seagate   | ST31500541AS       | 1.5 TB | 6       | 810   | 99    | 1.23   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 1       | 446   | 0     | 1.22   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 7       | 442   | 0     | 1.21   |
| Hitachi   | HDT725032VLA380    | 320 GB | 2       | 441   | 0     | 1.21   |
| Seagate   | ST9250315AS        | 250 GB | 4       | 609   | 253   | 1.21   |
| WDC       | WD2000JS-55MHB0    | 192 GB | 1       | 439   | 0     | 1.20   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 4       | 437   | 0     | 1.20   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 3       | 509   | 3     | 1.20   |
| Seagate   | ST9160412ASG       | 160 GB | 1       | 436   | 0     | 1.20   |
| WDC       | WD7500BPKX-22HPJT0 | 752 GB | 1       | 434   | 0     | 1.19   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 2       | 936   | 518   | 1.18   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 1       | 429   | 0     | 1.18   |
| WDC       | WD10JPVX-00JC3T0   | 1 TB   | 2       | 429   | 0     | 1.18   |
| Fujitsu   | MHT2080AH          | 80 GB  | 1       | 427   | 0     | 1.17   |
| Hitachi   | HDS721050CLA362    | 500 GB | 2       | 426   | 0     | 1.17   |
| Seagate   | ST3160815AS        | 160 GB | 3       | 1160  | 11    | 1.17   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 1       | 424   | 0     | 1.16   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 1       | 422   | 0     | 1.16   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 10      | 410   | 0     | 1.13   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 1       | 409   | 0     | 1.12   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 4       | 406   | 0     | 1.11   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 2       | 406   | 0     | 1.11   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 2       | 404   | 0     | 1.11   |
| Seagate   | ST9250410ASG       | 250 GB | 2       | 404   | 0     | 1.11   |
| HGST      | HUS722T2TALA604    | 2 TB   | 4       | 544   | 4     | 1.11   |
| Hitachi   | HTS723220L9A360    | 200 GB | 1       | 401   | 0     | 1.10   |
| Toshiba   | HDWD130            | 3 TB   | 7       | 395   | 0     | 1.08   |
| WDC       | WD1600BEVT-11ZCT0  | 160 GB | 1       | 392   | 0     | 1.07   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 16      | 445   | 8     | 1.07   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 1       | 1545  | 3     | 1.06   |
| Seagate   | ST380811AS         | 80 GB  | 1       | 383   | 0     | 1.05   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 7       | 441   | 2     | 1.05   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 1       | 382   | 0     | 1.05   |
| HGST      | HUS726020ALA610    | 2 TB   | 1       | 381   | 0     | 1.04   |
| WDC       | WD5000HHTZ-75N21V0 | 500 GB | 1       | 380   | 0     | 1.04   |
| Toshiba   | MK1517GAP          | 16 GB  | 1       | 380   | 0     | 1.04   |
| Seagate   | ST3500830AS        | 500 GB | 1       | 376   | 0     | 1.03   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 2       | 376   | 0     | 1.03   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 2       | 375   | 0     | 1.03   |
| WDC       | WD40NMZW-59GX6S1   | 4 TB   | 2       | 373   | 0     | 1.02   |
| Seagate   | ST9160821A         | 160 GB | 1       | 371   | 0     | 1.02   |
| HPE       | MB4000GCWLV        | 4 TB   | 4       | 366   | 0     | 1.00   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 3       | 544   | 196   | 1.00   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 6       | 484   | 3     | 0.99   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 1       | 2532  | 6     | 0.99   |
| Seagate   | ST3250620AS        | 250 GB | 1       | 1081  | 2     | 0.99   |
| WDC       | WD2500BEVS-22UST0  | 250 GB | 1       | 357   | 0     | 0.98   |
| Fujitsu   | MHZ2120BH G2       | 120 GB | 1       | 357   | 0     | 0.98   |
| Seagate   | ST500LX025-1U717D  | 500 GB | 2       | 355   | 0     | 0.97   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 4       | 353   | 0     | 0.97   |
| Seagate   | ST3120827AS        | 120 GB | 1       | 348   | 0     | 0.95   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 7       | 346   | 0     | 0.95   |
| Toshiba   | MN07ACA12T         | 12 TB  | 2       | 345   | 0     | 0.95   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 1       | 341   | 0     | 0.94   |
| Seagate   | ST2000NE0025-2F... | 2 TB   | 2       | 338   | 0     | 0.93   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 2       | 336   | 0     | 0.92   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 1       | 1677  | 4     | 0.92   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 2       | 330   | 0     | 0.91   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 1       | 328   | 0     | 0.90   |
| Toshiba   | MK3259GSXP         | 320 GB | 1       | 326   | 0     | 0.89   |
| MediaMax  | WL2000GSA6454      | 2 TB   | 3       | 697   | 6     | 0.89   |
| WDC       | WD20NMVW-59EDZS7   | 2 TB   | 1       | 320   | 0     | 0.88   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 1       | 315   | 0     | 0.87   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 1       | 311   | 0     | 0.85   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 4       | 387   | 2     | 0.85   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 5       | 308   | 0     | 0.85   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 5       | 354   | 152   | 0.84   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 2       | 302   | 0     | 0.83   |
| Fujitsu   | MJA2250BH FFS G1   | 250 GB | 1       | 302   | 0     | 0.83   |
| Hitachi   | HTS547550A9E384    | 500 GB | 4       | 559   | 294   | 0.83   |
| HGST      | HTS545050A7E680    | 500 GB | 3       | 301   | 0     | 0.83   |
| WDC       | WD7500AAVS-00D7B0  | 752 GB | 1       | 300   | 0     | 0.82   |
| Toshiba   | MQ01ACF032         | 320 GB | 1       | 299   | 0     | 0.82   |
| Toshiba   | DT01ACA050 LENOVO  | 500 GB | 1       | 298   | 0     | 0.82   |
| Seagate   | ST3250823AS        | 250 GB | 1       | 2661  | 8     | 0.81   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 5       | 292   | 0     | 0.80   |
| Toshiba   | MK2546GSX_200      | 200 GB | 1       | 291   | 0     | 0.80   |
| Samsung   | HM250HI            | 250 GB | 1       | 291   | 0     | 0.80   |
| Toshiba   | MQ01ABF032         | 320 GB | 2       | 289   | 0     | 0.79   |
| WDC       | WD5000LPLX-60ZNTT1 | 500 GB | 1       | 288   | 0     | 0.79   |
| HGST      | HTS725050A7E630    | 500 GB | 12      | 578   | 442   | 0.79   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 12      | 285   | 0     | 0.78   |
| Toshiba   | HDWQ140            | 4 TB   | 7       | 285   | 0     | 0.78   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 5       | 280   | 0     | 0.77   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 2       | 1571  | 6     | 0.77   |
| Toshiba   | MQ03UBB200         | 2 TB   | 2       | 269   | 0     | 0.74   |
| WDC       | WD3200BPVT-75JJ5T0 | 320 GB | 1       | 1075  | 3     | 0.74   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 3       | 267   | 0     | 0.73   |
| Hitachi   | HTS547575A9E384    | 752 GB | 2       | 476   | 514   | 0.73   |
| WDC       | WD3200BPVT-24JJ5T0 | 320 GB | 1       | 266   | 0     | 0.73   |
| Seagate   | ST9500325AS        | 500 GB | 8       | 690   | 153   | 0.73   |
| WDC       | WD1600BEVT-22ZCT0  | 160 GB | 7       | 331   | 3     | 0.72   |
| Seagate   | ST3750640NS        | 752 GB | 2       | 2066  | 1043  | 0.71   |
| Seagate   | ST3250410AS        | 250 GB | 2       | 409   | 3     | 0.70   |
| WDC       | WD5000LPCX-75VHAT0 | 500 GB | 1       | 254   | 0     | 0.70   |
| Seagate   | ST3120211AS        | 120 GB | 1       | 508   | 1     | 0.70   |
| Samsung   | HD403LJ            | 400 GB | 1       | 254   | 0     | 0.70   |
| Samsung   | HN-M101MBB         | 1 TB   | 2       | 251   | 0     | 0.69   |
| WDC       | WD5000LPVT-24G33T1 | 500 GB | 1       | 249   | 0     | 0.68   |
| WDC       | WD1600BEVS-08VAT2  | 160 GB | 3       | 404   | 1     | 0.68   |
| Toshiba   | HDWE160            | 6 TB   | 3       | 247   | 0     | 0.68   |
| Toshiba   | MK1060GSCX         | 100 GB | 1       | 247   | 0     | 0.68   |
| WDC       | WD40E31X-00HY4A0   | 4 TB   | 1       | 245   | 0     | 0.67   |
| WDC       | WD20SDZW-11JJ8S0   | 2 TB   | 1       | 244   | 0     | 0.67   |
| Seagate   | ST380215A          | 80 GB  | 1       | 242   | 0     | 0.66   |
| Seagate   | ST31000340NS       | 1 TB   | 1       | 2906  | 11    | 0.66   |
| Fujitsu   | MHT2080BH          | 80 GB  | 1       | 241   | 0     | 0.66   |
| WDC       | WD7500BPVT-80HXZT3 | 752 GB | 2       | 566   | 4     | 0.65   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 7       | 235   | 0     | 0.65   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 2       | 233   | 0     | 0.64   |
| Apple     | HDD ST2000DM001    | 2 TB   | 1       | 232   | 0     | 0.64   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 6       | 231   | 0     | 0.64   |
| Samsung   | SP2514N            | 250 GB | 1       | 2529  | 10    | 0.63   |
| HGST      | HTS541075A7E630    | 752 GB | 2       | 321   | 507   | 0.62   |
| Hitachi   | HTE723225A7A364    | 250 GB | 1       | 227   | 0     | 0.62   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 1       | 678   | 2     | 0.62   |
| Apple     | HDD HTS545050A7... | 500 GB | 2       | 225   | 0     | 0.62   |
| Hitachi   | HTS543232L9A300    | 320 GB | 1       | 223   | 0     | 0.61   |
| WDC       | WD40NDZW-11MR8S1   | 4 TB   | 1       | 222   | 0     | 0.61   |
| Toshiba   | HDWD120            | 2 TB   | 5       | 222   | 0     | 0.61   |
| Seagate   | ST1000LX015-1U7172 | 1 TB   | 3       | 279   | 1344  | 0.60   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 1       | 652   | 2     | 0.60   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 1       | 216   | 0     | 0.59   |
| Toshiba   | HDWD110            | 1 TB   | 9       | 216   | 0     | 0.59   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 7       | 214   | 0     | 0.59   |
| Seagate   | ST500LM000-1EJ162  | 500 GB | 3       | 213   | 0     | 0.58   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 5       | 342   | 527   | 0.58   |
| Seagate   | ST3160813AS        | 160 GB | 1       | 1056  | 4     | 0.58   |
| Toshiba   | MQ01ABD100         | 1 TB   | 14      | 313   | 144   | 0.57   |
| WDC       | WD20EARX-00ZUDB0   | 2 TB   | 1       | 2266  | 10    | 0.56   |
| WDC       | WD3200BPVT-75ZEST0 | 320 GB | 2       | 218   | 1     | 0.56   |
| Fujitsu   | MHZ2320BH FFS G1   | 320 GB | 1       | 203   | 0     | 0.56   |
| Hitachi   | HTS545032B9A302    | 320 GB | 1       | 605   | 2     | 0.55   |
| Apple     | HDD HTS541010A9... | 1 TB   | 1       | 1008  | 4     | 0.55   |
| Toshiba   | MQ04UBB400         | 4 TB   | 1       | 201   | 0     | 0.55   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 2       | 199   | 0     | 0.55   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 4       | 237   | 1     | 0.54   |
| Hitachi   | HTS541680J9SA00    | 80 GB  | 2       | 673   | 18    | 0.54   |
| WDC       | WD10SPZX-22Z10T0   | 1 TB   | 1       | 197   | 0     | 0.54   |
| Seagate   | ST9320421ASG       | 320 GB | 1       | 195   | 0     | 0.54   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 1       | 195   | 0     | 0.54   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 4       | 278   | 2     | 0.53   |
| Toshiba   | MK1234GSX          | 120 GB | 2       | 194   | 0     | 0.53   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 1       | 191   | 0     | 0.52   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 12      | 188   | 0     | 0.52   |
| Seagate   | ST1000VM002-1SD102 | 1 TB   | 2       | 187   | 0     | 0.51   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 5       | 1433  | 307   | 0.51   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 2       | 185   | 0     | 0.51   |
| ExcelStor | J8160S             | 160 GB | 2       | 1003  | 15    | 0.51   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 1       | 183   | 0     | 0.50   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 3       | 183   | 0     | 0.50   |
| WDC       | WD4000BEVT-00ZAT0  | 400 GB | 1       | 179   | 0     | 0.49   |
| WDC       | WD7500BPKX-80HPJT0 | 752 GB | 1       | 178   | 0     | 0.49   |
| WDC       | WD20SPZX-22CRAT0   | 2 TB   | 1       | 177   | 0     | 0.49   |
| WDC       | WD5000LPVX-75V0TT0 | 500 GB | 1       | 173   | 0     | 0.48   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 2       | 173   | 0     | 0.48   |
| WDC       | WD1600AAJS-75M0A0  | 160 GB | 1       | 510   | 2     | 0.47   |
| Hitachi   | HDT721064SLA360    | 640 GB | 1       | 169   | 0     | 0.46   |
| Toshiba   | MK5065GSXF         | 500 GB | 2       | 168   | 0     | 0.46   |
| Toshiba   | MK2555GSX          | 250 GB | 2       | 946   | 4     | 0.46   |
| Samsung   | HM160HI            | 160 GB | 2       | 580   | 18    | 0.46   |
| Seagate   | ST3500320NS        | 500 GB | 1       | 1324  | 7     | 0.45   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 1       | 163   | 0     | 0.45   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 2       | 161   | 0     | 0.44   |
| Fujitsu   | MJA2250BH G2       | 250 GB | 1       | 161   | 0     | 0.44   |
| WDC       | WD3200AAJS-22B4A0  | 320 GB | 1       | 1449  | 8     | 0.44   |
| Toshiba   | MQ01ABD050         | 500 GB | 3       | 356   | 686   | 0.44   |
| Toshiba   | MK1255GSX H        | 120 GB | 1       | 160   | 0     | 0.44   |
| WDC       | WD800BB-00HEA0     | 80 GB  | 1       | 4322  | 26    | 0.44   |
| Hitachi   | HTS545032B9A300    | 320 GB | 4       | 294   | 348   | 0.43   |
| WDC       | WD1003FBYX-88 LEN  | 1 TB   | 1       | 466   | 2     | 0.43   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 1       | 1390  | 8     | 0.42   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 13      | 507   | 629   | 0.42   |
| Seagate   | ST9750423AS        | 752 GB | 2       | 152   | 0     | 0.42   |
| Samsung   | HM320II            | 320 GB | 1       | 152   | 0     | 0.42   |
| WDC       | WD5000AVCS-632DY1  | 500 GB | 1       | 1354  | 8     | 0.41   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 1       | 148   | 0     | 0.41   |
| WDC       | WD3200AAKX-753CA1  | 320 GB | 1       | 147   | 0     | 0.40   |
| WDC       | WD3200BEVT-22ZCT0  | 320 GB | 2       | 198   | 6     | 0.39   |
| WDC       | WD800JB-00JJC0     | 80 GB  | 1       | 2710  | 18    | 0.39   |
| WDC       | WD60EMAZ-11LW3B0   | 6 TB   | 1       | 142   | 0     | 0.39   |
| Toshiba   | HDWE140            | 4 TB   | 4       | 184   | 5     | 0.39   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 3       | 332   | 2     | 0.37   |
| WDC       | WD2500AAKS-60L9A0  | 250 GB | 1       | 1350  | 9     | 0.37   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 3       | 134   | 0     | 0.37   |
| Toshiba   | DT01ABA300         | 3 TB   | 2       | 236   | 4     | 0.37   |
| WDC       | WD10JMVW-11AJGS1   | 1 TB   | 1       | 1298  | 9     | 0.36   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 4       | 129   | 0     | 0.36   |
| WDC       | WD5000AAKS-22V1A0  | 500 GB | 1       | 1163  | 8     | 0.35   |
| HGST      | HTS541010B7E610    | 1 TB   | 3       | 124   | 0     | 0.34   |
| WDC       | WD6400AAKS-22A7B0  | 640 GB | 1       | 1112  | 8     | 0.34   |
| WDC       | WD10EURX-83UY4Y0   | 1 TB   | 1       | 121   | 0     | 0.33   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 8       | 134   | 1     | 0.33   |
| Seagate   | ST3120026A         | 120 GB | 1       | 1076  | 8     | 0.33   |
| Seagate   | ST9500420AS        | 500 GB | 6       | 796   | 1058  | 0.33   |
| Hitachi   | HTS723232A7A364    | 320 GB | 4       | 800   | 766   | 0.32   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 16      | 132   | 57    | 0.32   |
| WDC       | WD10JPLX-00MBPT1   | 1 TB   | 1       | 114   | 0     | 0.31   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 1       | 571   | 4     | 0.31   |
| Seagate   | ST9120822AS        | 120 GB | 1       | 1028  | 8     | 0.31   |
| Toshiba   | MK1665GSX          | 160 GB | 1       | 114   | 0     | 0.31   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 5       | 113   | 0     | 0.31   |
| Seagate   | ST9500530NS 42D... | 500 GB | 2       | 221   | 48    | 0.31   |
| Seagate   | ST500LM000-SSHD... | 500 GB | 2       | 536   | 505   | 0.30   |
| WDC       | WD20SPZX-75UA7T0   | 2 TB   | 1       | 109   | 0     | 0.30   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 3       | 109   | 0     | 0.30   |
| WDC       | WD10SPZX-08Z10     | 1 TB   | 2       | 108   | 0     | 0.30   |
| WDC       | WD10SDRW-34A0XS0   | 1 TB   | 1       | 106   | 0     | 0.29   |
| WDC       | WD3200BEVT-00A0RT0 | 320 GB | 1       | 946   | 8     | 0.29   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 1       | 103   | 0     | 0.28   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 1       | 1338  | 12    | 0.28   |
| HGST      | HUH721010ALE604    | 10 TB  | 2       | 102   | 0     | 0.28   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 6       | 454   | 300   | 0.28   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 7       | 138   | 21    | 0.28   |
| Toshiba   | MK7575GSX          | 752 GB | 1       | 604   | 5     | 0.28   |
| Toshiba   | MQ01ACF050         | 500 GB | 2       | 100   | 0     | 0.28   |
| WDC       | WD120EDAZ-11F3RA0  | 12 TB  | 8       | 99    | 0     | 0.27   |
| Samsung   | HN-M500MBB         | 500 GB | 1       | 97    | 0     | 0.27   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 2       | 2329  | 118   | 0.26   |
| Hitachi   | HTS543225L9A300    | 250 GB | 2       | 525   | 5     | 0.25   |
| Seagate   | ST9250827AS        | 250 GB | 2       | 533   | 17    | 0.25   |
| Seagate   | ST500LT035-1E9G42  | 500 GB | 1       | 89    | 0     | 0.24   |
| Seagate   | ST31000528AS       | 1 TB   | 4       | 963   | 55    | 0.24   |
| WDC       | WD1600AAJS-00WAA0  | 160 GB | 2       | 97    | 1     | 0.24   |
| Toshiba   | MQ01ABF050         | 500 GB | 7       | 175   | 2     | 0.24   |
| Seagate   | STEC PATA          | 8 GB   | 1       | 87    | 0     | 0.24   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 3       | 393   | 6     | 0.24   |
| Hitachi   | HTS543232A7A384    | 320 GB | 4       | 275   | 280   | 0.24   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 6       | 170   | 1     | 0.23   |
| Toshiba   | MQ04ABF100         | 1 TB   | 8       | 98    | 1     | 0.23   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 1       | 82    | 0     | 0.23   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 2       | 163   | 1     | 0.22   |
| WDC       | WD60EZRZ-22GZ5B1   | 6 TB   | 1       | 81    | 0     | 0.22   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 1       | 161   | 1     | 0.22   |
| Seagate   | ST4000NM002A-2H... | 4 TB   | 2       | 79    | 0     | 0.22   |
| WDC       | WUH721414ALE6L4    | 14 TB  | 1       | 79    | 0     | 0.22   |
| Toshiba   | MQ01ABD075         | 752 GB | 1       | 692   | 8     | 0.21   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 1       | 2216  | 28    | 0.21   |
| WDC       | WD5000BPVX-00JC3T0 | 500 GB | 1       | 76    | 0     | 0.21   |
| Seagate   | ST1000LM014-1EJ164 | 1 TB   | 2       | 280   | 22    | 0.20   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 1       | 650   | 8     | 0.20   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 1       | 71    | 0     | 0.20   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 5       | 71    | 0     | 0.20   |
| WDC       | WD3200BPVT-55ZEST0 | 320 GB | 1       | 142   | 1     | 0.20   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 2       | 71    | 0     | 0.20   |
| Toshiba   | MK6006GAH          | 64 GB  | 1       | 426   | 5     | 0.19   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 8       | 69    | 0     | 0.19   |
| WDC       | WD5000LPCX-24C6HT0 | 500 GB | 1       | 68    | 0     | 0.19   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 1       | 67    | 0     | 0.18   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 2       | 65    | 0     | 0.18   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 4       | 411   | 757   | 0.17   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 2       | 61    | 0     | 0.17   |
| WDC       | WD20SPZX-22UA7T0   | 2 TB   | 5       | 61    | 0     | 0.17   |
| Apple     | HDD HTS541010A9... | 1 TB   | 1       | 61    | 0     | 0.17   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 1       | 343   | 5     | 0.16   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 1       | 284   | 4     | 0.16   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 1       | 56    | 0     | 0.15   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 1       | 55    | 0     | 0.15   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 1       | 52    | 0     | 0.14   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 1       | 1954  | 37    | 0.14   |
| WDC       | WD3200BEKT-60V5T1  | 320 GB | 1       | 102   | 1     | 0.14   |
| WDC       | WD2503ABYZ-011FA0  | 256 GB | 1       | 50    | 0     | 0.14   |
| Seagate   | ST3250820AS        | 250 GB | 1       | 392   | 7     | 0.13   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 2       | 48    | 0     | 0.13   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 2       | 48    | 0     | 0.13   |
| HGST      | HTS545032A7E380    | 320 GB | 3       | 448   | 7     | 0.13   |
| WDC       | WD5000LUCT-63C26Y0 | 500 GB | 1       | 45    | 0     | 0.12   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 4       | 43    | 0     | 0.12   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 1       | 388   | 8     | 0.12   |
| WDC       | WD20EVDS-63T3B0    | 2 TB   | 1       | 385   | 8     | 0.12   |
| Seagate   | ST750LM022 HN-M... | 752 GB | 2       | 313   | 1700  | 0.12   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 1       | 41    | 0     | 0.11   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 6       | 39    | 0     | 0.11   |
| WDC       | WD200EB-00BHF0     | 20 GB  | 1       | 273   | 6     | 0.11   |
| WDC       | WD3200BEVT-60ZCT1  | 320 GB | 1       | 428   | 10    | 0.11   |
| WDC       | WD120EFAX-68UNTN0  | 12 TB  | 2       | 38    | 0     | 0.11   |
| Seagate   | ST9500620NS        | 500 GB | 1       | 2829  | 73    | 0.10   |
| Toshiba   | MQ01ABD032         | 320 GB | 1       | 942   | 24    | 0.10   |
| WDC       | WD6400BEVT-22A0RT0 | 640 GB | 1       | 261   | 6     | 0.10   |
| Hitachi   | HTS541060G9SA00    | 64 GB  | 1       | 255   | 6     | 0.10   |
| Seagate   | ST500VT000-1DK142  | 500 GB | 1       | 71    | 1     | 0.10   |
| WDC       | WD2002FYPS-01U1B1  | 2 TB   | 1       | 1621  | 45    | 0.10   |
| Fujitsu   | MHS2040AT D        | 40 GB  | 1       | 1334  | 37    | 0.10   |
| Samsung   | HM320JI            | 320 GB | 2       | 297   | 8     | 0.09   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 1       | 33    | 0     | 0.09   |
| WDC       | WD4001FAEX-00MJRA0 | 4 TB   | 2       | 676   | 991   | 0.09   |
| Seagate   | ST1000DX001-1CM162 | 1 TB   | 1       | 671   | 19    | 0.09   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 1       | 31    | 0     | 0.09   |
| WDC       | WD10EADS-00P8B0    | 1 TB   | 1       | 279   | 8     | 0.08   |
| Hitachi   | HDP725050GLA360    | 500 GB | 1       | 1174  | 38    | 0.08   |
| Seagate   | ST9320320AS        | 320 GB | 1       | 719   | 23    | 0.08   |
| Seagate   | ST9320325AS        | 320 GB | 3       | 967   | 117   | 0.08   |
| Toshiba   | MG04ACA600E        | 6 TB   | 1       | 28    | 0     | 0.08   |
| Toshiba   | MK6475GSX          | 640 GB | 1       | 2340  | 83    | 0.08   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 5       | 514   | 1091  | 0.07   |
| Maxtor    | STM3320613AS       | 320 GB | 1       | 1639  | 61    | 0.07   |
| HGST      | HUS726060ALE610    | 6 TB   | 2       | 25    | 0     | 0.07   |
| WDC       | WD1200JS-00MHB1    | 120 GB | 1       | 437   | 17    | 0.07   |
| Toshiba   | MK2552GSX          | 250 GB | 1       | 23    | 0     | 0.06   |
| Hitachi   | HTS725025A9A364    | 250 GB | 2       | 297   | 523   | 0.06   |
| Maxtor    | 6L160M0            | 163 GB | 1       | 21    | 0     | 0.06   |
| WDC       | WD3200BEVE-00A0HT0 | 320 GB | 1       | 20    | 0     | 0.05   |
| WDC       | WD10EARX-22N0YB0   | 1 TB   | 1       | 175   | 8     | 0.05   |
| WDC       | WD10SPZX-22Z10T1   | 1 TB   | 1       | 19    | 0     | 0.05   |
| WDC       | WD10SPZX-24Z10     | 1 TB   | 5       | 36    | 1     | 0.05   |
| Seagate   | ST95005620AS       | 500 GB | 2       | 207   | 11    | 0.05   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 1       | 17    | 0     | 0.05   |
| Hitachi   | HTS548040M9AT00    | 40 GB  | 1       | 33    | 1     | 0.05   |
| Seagate   | ST3160812A         | 160 GB | 1       | 1810  | 107   | 0.05   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 9       | 16    | 0     | 0.05   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 1       | 16    | 0     | 0.04   |
| WDC       | WD2500BEVT-80A23T0 | 250 GB | 1       | 425   | 26    | 0.04   |
| Toshiba   | HDWD105            | 500 GB | 2       | 1701  | 286   | 0.04   |
| Seagate   | ST31500341AS       | 1.5 TB | 2       | 137   | 7     | 0.04   |
| HGST      | HUS726040ALA610    | 4 TB   | 1       | 1058  | 78    | 0.04   |
| Seagate   | ST1000LM025 HN-... | 1 TB   | 1       | 117   | 9     | 0.03   |
| Samsung   | HM080HI            | 80 GB  | 1       | 627   | 56    | 0.03   |
| Seagate   | ST9250320AS        | 250 GB | 1       | 241   | 22    | 0.03   |
| Toshiba   | MK3265GSXN         | 320 GB | 1       | 113   | 10    | 0.03   |
| Hitachi   | HTS543225A7A384    | 250 GB | 1       | 237   | 23    | 0.03   |
| Toshiba   | MK5061GSYN         | 500 GB | 2       | 20    | 6     | 0.02   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 1       | 80    | 8     | 0.02   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 2       | 8     | 0     | 0.02   |
| WDC       | WD1600BEVS-60RST0  | 160 GB | 1       | 164   | 18    | 0.02   |
| Hitachi   | HTS541612J9SA00    | 120 GB | 3       | 374   | 68    | 0.02   |
| WDC       | WD100EZAZ-11TDBA0  | 10 TB  | 1       | 8     | 0     | 0.02   |
| Hitachi   | HTS545050A7E380    | 500 GB | 2       | 186   | 181   | 0.02   |
| Toshiba   | MQ03UBB300         | 3 TB   | 1       | 8     | 0     | 0.02   |
| Hitachi   | HTS543212L9A300    | 120 GB | 2       | 1802  | 550   | 0.02   |
| Hitachi   | HDP725016GLA380    | 160 GB | 1       | 1804  | 250   | 0.02   |
| Seagate   | ST32500NSSUN250G   | 250 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | HM321HI            | 320 GB | 2       | 100   | 433   | 0.02   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 1       | 2670  | 395   | 0.02   |
| WDC       | WD2500BEVT-60A23T0 | 250 GB | 1       | 250   | 37    | 0.02   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 4       | 6     | 0     | 0.02   |
| Toshiba   | MQ02ABF050H-SSH... | 500 GB | 1       | 540   | 93    | 0.02   |
| WDC       | WD10JPVX-75JC3T0   | 1 TB   | 3       | 469   | 125   | 0.02   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 1       | 450   | 78    | 0.02   |
| Toshiba   | MK8025GAS          | 80 GB  | 1       | 5     | 0     | 0.01   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 1       | 349   | 69    | 0.01   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 1       | 4     | 0     | 0.01   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 1       | 100   | 21    | 0.01   |
| WDC       | WD3200BEVT-60ZCT0  | 320 GB | 1       | 133   | 29    | 0.01   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 1       | 1809  | 456   | 0.01   |
| Seagate   | ST3160815A         | 160 GB | 1       | 4054  | 1048  | 0.01   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 16      | 3     | 0     | 0.01   |
| WDC       | WD5000AAKS-60WWPA0 | 500 GB | 1       | 798   | 241   | 0.01   |
| Hitachi   | HTS543216L9A300    | 160 GB | 1       | 1644  | 522   | 0.01   |
| WDC       | WD10JMVW-11AJGS0   | 1 TB   | 1       | 27    | 10    | 0.01   |
| Seagate   | ST2000DL001-9VT156 | 2 TB   | 1       | 2429  | 1010  | 0.01   |
| Toshiba   | MK2018GAP          | 20 GB  | 1       | 126   | 55    | 0.01   |
| HGST      | HTS725025A7E630    | 250 GB | 1       | 43    | 20    | 0.01   |
| Seagate   | ST3500514NS        | 500 GB | 1       | 205   | 103   | 0.01   |
| Maxtor    | 6Y080P0            | 82 GB  | 3       | 15    | 413   | 0.01   |
| Seagate   | ST31000333AS       | 1 TB   | 1       | 316   | 164   | 0.01   |
| Seagate   | ST320DM000-1BD14C  | 320 GB | 1       | 1890  | 1006  | 0.01   |
| WDC       | WD40EZAZ-00SF3B0   | 4 TB   | 1       | 1     | 0     | 0.01   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 1       | 1     | 0     | 0.00   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 1       | 1914  | 1089  | 0.00   |
| WDC       | WD2005FBYZ-01YCBB3 | 2 TB   | 2       | 1     | 0     | 0.00   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | WD2500JS-22NCB1    | 250 GB | 1       | 1197  | 1038  | 0.00   |
| WDC       | WD1600BEVS-00UST0  | 160 GB | 1       | 87    | 76    | 0.00   |
| Hitachi   | HDS721050CLA660    | 500 GB | 1       | 1080  | 1015  | 0.00   |
| Seagate   | ST980816AS         | 80 GB  | 1       | 446   | 494   | 0.00   |
| Hitachi   | HDS723015BLA642    | 1.5 TB | 1       | 902   | 1016  | 0.00   |
| Hitachi   | HCC543225A7A380    | 250 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | ST9160314AS        | 160 GB | 1       | 684   | 1062  | 0.00   |
| Hitachi   | HTS723216L9A360    | 160 GB | 1       | 646   | 1013  | 0.00   |
| Samsung   | HD642JJ            | 640 GB | 1       | 662   | 1161  | 0.00   |
| Hitachi   | HTS725050A9A364    | 500 GB | 1       | 862   | 1522  | 0.00   |
| Fujitsu   | MHW2160BH          | 160 GB | 1       | 475   | 957   | 0.00   |
| Samsung   | HM500LI            | 500 GB | 1       | 1476  | 3036  | 0.00   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 1       | 165   | 372   | 0.00   |
| Hitachi   | HTS545050B9A300    | 500 GB | 1       | 458   | 1045  | 0.00   |
| Seagate   | ST320LT012-9WS14C  | 320 GB | 1       | 761   | 2087  | 0.00   |
| Hitachi   | HTS725032A7E630    | 320 GB | 1       | 348   | 1025  | 0.00   |
| Seagate   | ST9320423AS        | 320 GB | 1       | 334   | 1009  | 0.00   |
| Seagate   | ST9160412AS        | 160 GB | 1       | 313   | 1009  | 0.00   |
| Seagate   | ST1000NM004A-2M... | 1 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD5000B            | 500 GB | 1       | 252   | 1011  | 0.00   |
| Seagate   | ST3160215AS        | 160 GB | 1       | 551   | 2350  | 0.00   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 10      | 0     | 0     | 0.00   |
| Toshiba   | MK2555GSXF         | 250 GB | 1       | 294   | 1456  | 0.00   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | HM121HI            | 120 GB | 1       | 501   | 3029  | 0.00   |
| Hitachi   | DK23AA-12          | 12 GB  | 1       | 4     | 31    | 0.00   |
| Samsung   | HD252HJ            | 250 GB | 1       | 173   | 1520  | 0.00   |
| HGST      | HTS541010A7E630    | 1 TB   | 1       | 96    | 1023  | 0.00   |
| Hitachi   | HCS5C1050CLA382    | 500 GB | 1       | 9     | 142   | 0.00   |
| Maxtor    | 6Y160M0            | 160 GB | 1       | 7     | 149   | 0.00   |
| Toshiba   | MK3261GSYN         | 320 GB | 1       | 3     | 139   | 0.00   |
| Maxtor    | 6E040L0            | 41 GB  | 1       | 20    | 1133  | 0.00   |
| Samsung   | HM250JI            | 250 GB | 1       | 16    | 1010  | 0.00   |
| Toshiba   | MK1059GSM          | 1 TB   | 1       | 8     | 558   | 0.00   |
| Hitachi   | HTS721060G9AT00    | 64 GB  | 1       | 0     | 37    | 0.00   |
| Toshiba   | MK3276GSX          | 320 GB | 1       | 2     | 1008  | 0.00   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| Seagate   | Barracuda ATA V        | 1      | 1       | 5214  | 0     | 14.29  |
| Hitachi   | Deskstar 7K500         | 1      | 1       | 3763  | 0     | 10.31  |
| Hitachi   | Sun Internal           | 1      | 2       | 2785  | 0     | 7.63   |
| Seagate   | Constellation ES.2 ... | 2      | 2       | 2666  | 0     | 7.31   |
| Hitachi   | Deskstar 7K1000.B      | 3      | 3       | 2495  | 0     | 6.84   |
| WDC       | RE3                    | 5      | 8       | 2689  | 1     | 6.78   |
| Maxtor    | DiamondMax 10 (SATA... | 1      | 1       | 2371  | 0     | 6.50   |
| Hitachi   | Deskstar 7K80          | 1      | 1       | 2086  | 0     | 5.72   |
| Samsung   | SpinPoint F3           | 2      | 7       | 2564  | 1     | 5.71   |
| Hitachi   | Deskstar 5K4000        | 1      | 21      | 2076  | 0     | 5.69   |
| Hitachi   | Deskstar 5K3000        | 1      | 18      | 2020  | 2     | 5.23   |
| Samsung   | SpinPoint F4 EG (AF)   | 1      | 14      | 2533  | 8     | 5.22   |
| Seagate   | DB35.3                 | 1      | 1       | 1863  | 0     | 5.11   |
| WDC       | AV                     | 2      | 4       | 1838  | 0     | 5.04   |
| WDC       | Caviar Black           | 14     | 38      | 2162  | 12    | 5.00   |
| HGST      | Ultrastar He8          | 1      | 1       | 1820  | 0     | 4.99   |
| WDC       | Caviar SE              | 14     | 19      | 2540  | 58    | 4.98   |
| Hitachi   | Travelstar 7K750       | 1      | 2       | 1757  | 0     | 4.82   |
| Hitachi   | Ultrastar 7K3000       | 3      | 15      | 1828  | 135   | 4.76   |
| Hitachi   | Ultrastar A7K1000      | 2      | 3       | 2579  | 1     | 4.73   |
| HP        | Proliant HardDrive     | 3      | 7       | 2752  | 2     | 4.48   |
| WDC       | Caviar Green           | 13     | 20      | 2172  | 133   | 4.45   |
| HGST      | Ultrastar 7K4000       | 2      | 11      | 1547  | 0     | 4.24   |
| Samsung   | SpinPoint T166         | 2      | 7       | 2668  | 2     | 4.19   |
| Maxtor    | DiamondMax Plus D740X  | 1      | 3       | 2093  | 2     | 4.15   |
| Seagate   | SpinPoint F4 EG (AF)   | 1      | 2       | 1504  | 0     | 4.12   |
| WDC       | Protege                | 2      | 2       | 1616  | 3     | 4.11   |
| Hitachi   | Deskstar E7K1000       | 1      | 3       | 3419  | 4     | 4.09   |
| HP        | Seagate Constellati... | 1      | 7       | 1962  | 4     | 4.08   |
| WDC       | Green                  | 16     | 42      | 1654  | 31    | 4.07   |
| Seagate   | Constellation ES.3     | 4      | 10      | 1478  | 0     | 4.05   |
| Seagate   | Constellation CS       | 2      | 5       | 1808  | 23    | 3.98   |
| WDC       | VelociRaptor           | 6      | 9       | 1476  | 1     | 3.89   |
| WDC       | RE                     | 4      | 10      | 1635  | 1     | 3.87   |
| Hitachi   | Deskstar 7K1000        | 2      | 10      | 1951  | 1     | 3.84   |
| Seagate   | NAS HDD                | 4      | 10      | 1380  | 0     | 3.78   |
| HGST      | Deskstar NAS           | 6      | 34      | 1523  | 24    | 3.75   |
| Seagate   | Barracuda XT           | 2      | 3       | 1361  | 0     | 3.73   |
| Hitachi   | Deskstar 7K160         | 2      | 2       | 1343  | 0     | 3.68   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 2      | 11      | 1339  | 0     | 3.67   |
| WDC       | RE4                    | 10     | 24      | 1391  | 1     | 3.65   |
| WDC       | Caviar SE16            | 1      | 1       | 1317  | 0     | 3.61   |
| Samsung   | SpinPoint F1 DT        | 7      | 17      | 1704  | 181   | 3.30   |
| Hitachi   | Deskstar T7K500        | 2      | 3       | 1187  | 0     | 3.25   |
| WDC       | Unknown                | 1      | 1       | 1179  | 0     | 3.23   |
| Seagate   | Barracuda ES           | 4      | 8       | 1796  | 261   | 3.21   |
| Maxtor    | DiamondMax 21          | 2      | 3       | 1125  | 0     | 3.08   |
| Hitachi   | Deskstar 5K1000        | 1      | 1       | 1122  | 0     | 3.08   |
| Seagate   | Desktop HDD.15         | 5      | 27      | 1226  | 39    | 3.05   |
| Seagate   | Archive HDD            | 1      | 5       | 1429  | 203   | 2.94   |
| Toshiba   | 2.5" HDD MQ01UBB       | 1      | 1       | 1067  | 0     | 2.93   |
| Hitachi   | Travelstar 5K250       | 1      | 3       | 1273  | 1     | 2.88   |
| Seagate   | Surveillance           | 2      | 3       | 1044  | 0     | 2.86   |
| Toshiba   | 2.5" HDD MQ01ABD..H    | 1      | 2       | 1041  | 0     | 2.85   |
| Toshiba   | 3.5" MG04ACA Enterp... | 2      | 3       | 1033  | 0     | 2.83   |
| WDC       | Raptor                 | 3      | 3       | 1098  | 2     | 2.80   |
| WDC       | Caviar                 | 4      | 5       | 2180  | 144   | 2.80   |
| WDC       | Caviar Blue            | 27     | 34      | 1206  | 9     | 2.76   |
| Seagate   | Momentus 7200.3        | 2      | 2       | 999   | 0     | 2.74   |
| Hitachi   | Ultrastar A7K2000      | 3      | 15      | 1349  | 30    | 2.70   |
| WDC       | Red                    | 20     | 268     | 1135  | 14    | 2.69   |
| Samsung   | SpinPoint F3 EG        | 1      | 1       | 959   | 0     | 2.63   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 1       | 953   | 0     | 2.61   |
| WDC       | Scorpio Black          | 11     | 13      | 987   | 1     | 2.60   |
| Seagate   | Barracuda 7200.7 an... | 6      | 11      | 1283  | 2     | 2.58   |
| CLOVER    | Hightech Utania        | 1      | 1       | 928   | 0     | 2.54   |
| Toshiba   | 2.5" HDD MQ04UBD       | 1      | 1       | 906   | 0     | 2.48   |
| Samsung   | SpinPoint F2 EG        | 3      | 10      | 1353  | 318   | 2.46   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 42      | 986   | 29    | 2.43   |
| Seagate   | Constellation ES (S... | 2      | 4       | 1827  | 9     | 2.37   |
| Seagate   | U6                     | 1      | 1       | 2579  | 2     | 2.36   |
| Seagate   | Barracuda 7200.12      | 9      | 50      | 1202  | 66    | 2.28   |
| Samsung   | SpinPoint M7           | 3      | 5       | 1035  | 42    | 2.27   |
| Seagate   | Pipeline HD 5900.2     | 2      | 8       | 825   | 0     | 2.26   |
| Lenovo    | RE                     | 1      | 4       | 802   | 0     | 2.20   |
| Seagate   | Skyhawk                | 2      | 8       | 901   | 1     | 2.16   |
| WDC       | Purple                 | 6      | 7       | 744   | 0     | 2.04   |
| Seagate   | Momentus 5400.2        | 1      | 1       | 741   | 0     | 2.03   |
| Seagate   | Barracuda 7200.14 (AF) | 17     | 101     | 983   | 160   | 2.01   |
| WDC       | Se                     | 1      | 1       | 734   | 0     | 2.01   |
| Toshiba   | 3.5" MD04ACA Enterp... | 1      | 1       | 732   | 0     | 2.01   |
| Hitachi   | Deskstar 7K2000        | 1      | 1       | 725   | 0     | 1.99   |
| Seagate   | Exos X12               | 1      | 1       | 710   | 0     | 1.95   |
| Samsung   | SpinPoint P120         | 2      | 2       | 1844  | 5     | 1.90   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 1      | 1       | 692   | 0     | 1.90   |
| Seagate   | Barracuda LP           | 3      | 9       | 1042  | 173   | 1.90   |
| Seagate   | Exos 7E2               | 1      | 1       | 684   | 0     | 1.88   |
| MaxDig... | Unknown                | 1      | 1       | 681   | 0     | 1.87   |
| WDC       | Blue                   | 50     | 122     | 750   | 11    | 1.80   |
| Toshiba   | X300                   | 4      | 14      | 715   | 4     | 1.70   |
| Hitachi   | Deskstar 7K4000        | 1      | 1       | 614   | 0     | 1.68   |
| Hitachi   | Deskstar 7K3000        | 3      | 3       | 912   | 339   | 1.68   |
| Seagate   | Barracuda Green (AF)   | 3      | 11      | 1525  | 394   | 1.67   |
| ExcelStor | Jupiter                | 2      | 4       | 1009  | 8     | 1.64   |
| WDC       | Ultrastar He10/12      | 3      | 14      | 598   | 0     | 1.64   |
| Toshiba   | Unknown                | 4      | 5       | 593   | 0     | 1.63   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 1       | 592   | 0     | 1.62   |
| Seagate   | Constellation.2 (SATA) | 2      | 3       | 1508  | 25    | 1.58   |
| HGST      | Travelstar 7K1000      | 1      | 13      | 589   | 79    | 1.56   |
| Hitachi   | Travelstar 5K500.B     | 7      | 13      | 716   | 233   | 1.55   |
| WDC       | Black Mobile           | 11     | 19      | 629   | 1     | 1.55   |
| Seagate   | Video 2.5              | 2      | 2       | 577   | 1     | 1.53   |
| HGST      | Ultrastar 7K6000       | 5      | 8       | 684   | 10    | 1.52   |
| Samsung   | SpinPoint P80 SD       | 1      | 1       | 547   | 0     | 1.50   |
| WDC       | Elements / My Passport | 11     | 15      | 688   | 71    | 1.48   |
| Seagate   | Barracuda 7200.10      | 13     | 21      | 1017  | 221   | 1.48   |
| IBM       | Travelstar 6GN         | 1      | 1       | 522   | 0     | 1.43   |
| WDC       | HGST Ultrastar He10    | 2      | 14      | 519   | 0     | 1.42   |
| Samsung   | SpinPoint S166         | 1      | 3       | 498   | 0     | 1.37   |
| Seagate   | Barracuda 3.5          | 5      | 33      | 659   | 140   | 1.36   |
| Seagate   | IronWolf Pro           | 4      | 8       | 581   | 1     | 1.34   |
| HGST      | Travelstar 5K1000      | 1      | 8       | 475   | 255   | 1.29   |
| HGST      | Ultrastar 7K2          | 2      | 5       | 575   | 4     | 1.27   |
| Fujitsu   | MHY BH                 | 1      | 2       | 456   | 0     | 1.25   |
| Seagate   | SpinPoint M8 (AF)      | 4      | 24      | 616   | 144   | 1.25   |
| WDC       | RE2                    | 1      | 1       | 455   | 0     | 1.25   |
| WDC       | Red Pro                | 5      | 12      | 485   | 2     | 1.16   |
| Toshiba   | N300 NAS HDD           | 2      | 15      | 407   | 0     | 1.12   |
| Fujitsu   | MJA BH                 | 5      | 5       | 397   | 0     | 1.09   |
| HGST      | Travelstar Z7K500      | 4      | 15      | 624   | 355   | 1.06   |
| WDC       | Scorpio Blue           | 34     | 48      | 473   | 6     | 1.01   |
| HPE       | Proliant HardDrive     | 1      | 4       | 366   | 0     | 1.00   |
| Seagate   | Enterprise Capacity... | 4      | 6       | 365   | 0     | 1.00   |
| Seagate   | BarraCuda 3.5          | 5      | 27      | 373   | 6     | 1.00   |
| WDC       | Black                  | 6      | 13      | 465   | 153   | 0.97   |
| Hitachi   | Deskstar P7K500        | 3      | 4       | 1214  | 73    | 0.97   |
| Seagate   | Barracuda 2.5 5400     | 5      | 33      | 379   | 1     | 0.97   |
| Hitachi   | Travelstar 7K320       | 3      | 3       | 564   | 338   | 0.96   |
| Toshiba   | Toshiba Client HDD     | 1      | 2       | 345   | 0     | 0.95   |
| Hitachi   | Ultrastar 7K4000       | 2      | 16      | 346   | 1     | 0.93   |
| Seagate   | Barracuda 7200.9       | 4      | 5       | 747   | 22    | 0.92   |
| Fujitsu   | MHT                    | 2      | 2       | 334   | 0     | 0.92   |
| Hitachi   | Deskstar 7K1000.C      | 6      | 8       | 1083  | 157   | 0.91   |
| Toshiba   | 2.5" HDD MK..59GSXP    | 1      | 1       | 326   | 0     | 0.89   |
| MediaMax  | WL2000                 | 1      | 3       | 697   | 6     | 0.89   |
| Fujitsu   | MHW BH                 | 2      | 2       | 558   | 479   | 0.88   |
| Toshiba   | 3.5" HDD DT01ACA       | 1      | 1       | 298   | 0     | 0.82   |
| Seagate   | Barracuda 7200.8       | 1      | 1       | 2661  | 8     | 0.81   |
| Hitachi   | Travelstar 5K750       | 2      | 6       | 531   | 367   | 0.80   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 2       | 289   | 0     | 0.79   |
| Seagate   | Barracuda Compute      | 1      | 12      | 285   | 0     | 0.78   |
| Seagate   | Momentus 7200.4        | 6      | 12      | 672   | 697   | 0.77   |
| Fujitsu   | MHZ BH                 | 2      | 2       | 280   | 0     | 0.77   |
| Hitachi   | Travelstar Z7K500      | 2      | 2       | 442   | 513   | 0.73   |
| Seagate   | SpinPoint M9T          | 1      | 3       | 267   | 0     | 0.73   |
| Toshiba   | P300                   | 4      | 23      | 401   | 25    | 0.70   |
| Seagate   | FireCuda 2.5           | 3      | 6       | 282   | 672   | 0.69   |
| Seagate   | Momentus 5400.6        | 4      | 16      | 721   | 228   | 0.68   |
| WDC       | Blue SSHD              | 1      | 1       | 245   | 0     | 0.67   |
| Seagate   | Momentus 5400.3        | 2      | 2       | 700   | 4     | 0.67   |
| Toshiba   | 2.5" HDD               | 4      | 5       | 264   | 11    | 0.66   |
| HGST      | Ultrastar HC310/320    | 1      | 2       | 233   | 0     | 0.64   |
| Apple     | Barracuda 7200.12      | 1      | 1       | 232   | 0     | 0.64   |
| Apple     | HGST Travelstar Z5K500 | 1      | 2       | 225   | 0     | 0.62   |
| Seagate   | Laptop SSHD            | 4      | 8       | 374   | 132   | 0.59   |
| WDC       | Blue Mobile            | 24     | 51      | 245   | 28    | 0.57   |
| Seagate   | Barracuda ES.2         | 2      | 2       | 2115  | 9     | 0.56   |
| Toshiba   | 2.5" HDD MQ04UBB       | 1      | 1       | 201   | 0     | 0.55   |
| Seagate   | IronWolf               | 8      | 53      | 218   | 1     | 0.55   |
| Samsung   | SpinPoint M8 (AF)      | 2      | 3       | 200   | 0     | 0.55   |
| WDC       | RE4-GP                 | 2      | 3       | 1588  | 19    | 0.54   |
| Hitachi   | Travelstar 7K100       | 2      | 2       | 772   | 20    | 0.53   |
| Seagate   | Momentus 5400.5        | 3      | 3       | 1187  | 17    | 0.51   |
| Toshiba   | 2.5" HDD MQ01ABD       | 4      | 19      | 373   | 216   | 0.51   |
| Toshiba   | 2.5" HDD MQ03UBB       | 2      | 3       | 182   | 0     | 0.50   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 3      | 4       | 185   | 38    | 0.49   |
| HGST      | Travelstar Z5K500      | 2      | 6       | 374   | 4     | 0.48   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 3       | 166   | 0     | 0.46   |
| Toshiba   | 2.5" HDD MK..55GSX     | 1      | 1       | 160   | 0     | 0.44   |
| Hitachi   | Travelstar 5K160       | 3      | 6       | 497   | 40    | 0.43   |
| Seagate   | Momentus 5400.7 (AF)   | 1      | 2       | 152   | 0     | 0.42   |
| WDC       | Internal Use HDD       | 2      | 2       | 152   | 0     | 0.42   |
| WDC       | Gold                   | 3      | 5       | 184   | 75    | 0.41   |
| Seagate   | Laptop HDD             | 5      | 26      | 531   | 674   | 0.41   |
| Seagate   | Video 3.5 HDD          | 3      | 4       | 595   | 114   | 0.39   |
| HGST      | Travelstar Z5K1000     | 3      | 6       | 185   | 340   | 0.38   |
| Hitachi   | Travelstar Z7K320      | 2      | 5       | 685   | 613   | 0.38   |
| Toshiba   | 3.5" DT01ABA Deskto... | 1      | 2       | 236   | 4     | 0.37   |
| Apple     | Travelstar 5K1000      | 2      | 2       | 534   | 2     | 0.36   |
| Toshiba   | 2.5" HDD MK..65GSX     | 3      | 4       | 141   | 3     | 0.32   |
| Seagate   | Mobile HDD             | 2      | 21      | 128   | 44    | 0.31   |
| Seagate   | Constellation          | 1      | 2       | 221   | 48    | 0.31   |
| Toshiba   | 2.5" HDD MK..55GSX     | 2      | 3       | 729   | 488   | 0.31   |
| WDC       | IU CB500               | 1      | 1       | 106   | 0     | 0.29   |
| WDC       | White Label            | 2      | 9       | 104   | 0     | 0.29   |
| Hitachi   | Travelstar 4K120       | 1      | 1       | 1338  | 12    | 0.28   |
| HGST      | Ultrastar He10         | 1      | 2       | 102   | 0     | 0.28   |
| Seagate   | Momentus 5400.4        | 1      | 2       | 533   | 17    | 0.25   |
| Seagate   | Ultra Mobile HDD       | 1      | 1       | 89    | 0     | 0.24   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 7       | 175   | 2     | 0.24   |
| Seagate   | Unknown                | 1      | 1       | 87    | 0     | 0.24   |
| WDC       | AV-GP                  | 4      | 4       | 473   | 4     | 0.24   |
| Seagate   | Barracuda Pro Compute  | 1      | 6       | 170   | 1     | 0.23   |
| Samsung   | SpinPoint M5           | 3      | 4       | 419   | 1019  | 0.23   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 8       | 98    | 1     | 0.23   |
| WDC       | Ultrastar DC HC530     | 1      | 1       | 79    | 0     | 0.22   |
| Toshiba   | 1.8" HDD               | 1      | 1       | 426   | 5     | 0.19   |
| Hitachi   | Travelstar Z5K320      | 2      | 5       | 267   | 229   | 0.19   |
| Hitachi   | Travelstar 5K320       | 5      | 7       | 1211  | 239   | 0.19   |
| Toshiba   | 2.5" HDD MK..75GSX     | 2      | 2       | 1472  | 44    | 0.18   |
| Seagate   | Momentus Thin          | 1      | 4       | 411   | 757   | 0.17   |
| Seagate   | Barracuda 7200.11      | 3      | 4       | 411   | 46    | 0.17   |
| Seagate   | Exos 7E8               | 2      | 3       | 53    | 0     | 0.15   |
| Seagate   | Exos X16               | 1      | 4       | 43    | 0     | 0.12   |
| Hitachi   | Travelstar 5K100       | 1      | 1       | 255   | 6     | 0.10   |
| Fujitsu   | MHS AT                 | 1      | 1       | 1334  | 37    | 0.10   |
| Seagate   | Desktop SSHD           | 1      | 1       | 671   | 19    | 0.09   |
| Maxtor    | DiamondMax 22          | 1      | 1       | 1639  | 61    | 0.07   |
| Toshiba   | 2.5" HDD MK..52GSX     | 1      | 1       | 23    | 0     | 0.06   |
| Samsung   | SpinPoint M6           | 2      | 3       | 690   | 1018  | 0.06   |
| Maxtor    | DiamondMax 10 (ATA/... | 1      | 1       | 21    | 0     | 0.06   |
| WDC       | Scorpio Blue EIDE      | 1      | 1       | 20    | 0     | 0.05   |
| Seagate   | Momentus XT            | 1      | 2       | 207   | 11    | 0.05   |
| Hitachi   | Travelstar 5K80        | 1      | 1       | 33    | 1     | 0.05   |
| Hitachi   | Travelstar 7K500       | 2      | 3       | 486   | 856   | 0.04   |
| Seagate   | SpinPoint M8U (USB)    | 1      | 1       | 117   | 9     | 0.03   |
| Samsung   | SpinPoint M40/60/80    | 1      | 1       | 627   | 56    | 0.03   |
| Hitachi   | Travelstar Z5K500      | 1      | 2       | 186   | 181   | 0.02   |
| Samsung   | SpinPoint M7E (AF)     | 1      | 2       | 100   | 433   | 0.02   |
| Toshiba   | MG07ACA Enterprise ... | 1      | 4       | 6     | 0     | 0.02   |
| Toshiba   | 2.5" HDD MQ02ABF..H    | 1      | 1       | 540   | 93    | 0.02   |
| Toshiba   | 2.5" HDD MQ02ABD..H    | 1      | 1       | 349   | 69    | 0.01   |
| Seagate   | Constellation ES (S... | 1      | 1       | 205   | 103   | 0.01   |
| Maxtor    | DiamondMax Plus 9      | 2      | 4       | 13    | 347   | 0.00   |
| Seagate   | Momentus 5400 FDE.2    | 1      | 1       | 446   | 494   | 0.00   |
| Hitachi   | CinemaStar Z5K320      | 1      | 1       | 0     | 0     | 0.00   |
| HGST      | MegaScale 4000         | 2      | 11      | 0     | 0     | 0.00   |
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

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| HP          | 4      | 14      | 2357  | 3     | 4.28   |
| Samsung     | 32     | 80      | 1645  | 183   | 3.12   |
| Hitachi     | 79     | 196     | 1317  | 111   | 2.82   |
| CLOVER      | 1      | 1       | 928   | 0     | 2.54   |
| WDC         | 324    | 845     | 1071  | 20    | 2.50   |
| Lenovo      | 1      | 4       | 802   | 0     | 2.20   |
| HGST        | 31     | 122     | 851   | 93    | 2.06   |
| Maxtor      | 9      | 14      | 983   | 185   | 2.02   |
| MaxDigital  | 1      | 1       | 681   | 0     | 1.87   |
| ExcelStor   | 2      | 4       | 1009  | 8     | 1.64   |
| Seagate     | 190    | 651     | 796   | 127   | 1.56   |
| IBM         | 1      | 1       | 522   | 0     | 1.43   |
| Toshiba     | 67     | 199     | 586   | 48    | 1.34   |
| HPE         | 1      | 4       | 366   | 0     | 1.00   |
| Fujitsu     | 13     | 14      | 470   | 71    | 0.94   |
| MediaMax    | 1      | 3       | 697   | 6     | 0.89   |
| Apple       | 4      | 5       | 350   | 1     | 0.52   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See complete list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| OCZ       | VERTEX2            | 64 GB  | 1       | 2937  | 0     | 8.05   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 1       | 2739  | 0     | 7.51   |
| Intel     | SSDMCEAC120B3      | 120 GB | 1       | 2735  | 0     | 7.49   |
| WDC       | WDBNCE5000PNC      | 500 GB | 1       | 2730  | 0     | 7.48   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 1       | 2655  | 0     | 7.28   |
| Corsair   | Force 3 SSD        | 240 GB | 1       | 2525  | 0     | 6.92   |
| Intel     | SSDSC2BB240G4      | 240 GB | 1       | 2392  | 0     | 6.56   |
| Corsair   | Force GS           | 128 GB | 1       | 2275  | 0     | 6.23   |
| Intel     | SSDSC2BB160G4      | 160 GB | 1       | 2147  | 0     | 5.88   |
| OCZ       | SOLID3             | 120 GB | 1       | 2144  | 0     | 5.87   |
| Corsair   | Force GT           | 240 GB | 1       | 1999  | 0     | 5.48   |
| Samsung   | MMCRE28G5MXP-0VB   | 128 GB | 1       | 1998  | 0     | 5.47   |
| HPE       | MK0400GCTZA        | 400 GB | 2       | 1980  | 0     | 5.43   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 1       | 1964  | 0     | 5.38   |
| Intel     | SSDSC2BF120A5      | 120 GB | 1       | 1960  | 0     | 5.37   |
| Samsung   | SSD 850 PRO        | 128 GB | 5       | 1921  | 0     | 5.27   |
| ADATA     | SP310              | 32 GB  | 2       | 1889  | 0     | 5.18   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 1       | 1861  | 0     | 5.10   |
| Samsung   | SSD PB22-JS3 TM    | 64 GB  | 1       | 1801  | 0     | 4.94   |
| OCZ       | AGILITY3           | 120 GB | 4       | 1857  | 302   | 4.92   |
| Intel     | SSDSC2BB240G6      | 240 GB | 2       | 1787  | 0     | 4.90   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 1       | 1656  | 0     | 4.54   |
| Intel     | SSDMCEAC030B3      | 32 GB  | 2       | 1641  | 0     | 4.50   |
| Intel     | SSDSA2CW120G3      | 120 GB | 3       | 1632  | 0     | 4.47   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 8       | 1632  | 0     | 4.47   |
| Samsung   | SSD 840 EVO        | 120 GB | 12      | 1932  | 30    | 4.42   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 2       | 1593  | 0     | 4.36   |
| Transcend | TS8GSSD500         | 8 GB   | 1       | 1520  | 0     | 4.17   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 3       | 1515  | 0     | 4.15   |
| Samsung   | SSD 840 PRO Series | 128 GB | 10      | 1584  | 2     | 4.11   |
| ADATA     | SP310              | 128 GB | 1       | 1488  | 0     | 4.08   |
| Samsung   | MZMTD128HAFV-000L1 | 128 GB | 1       | 1487  | 0     | 4.08   |
| Samsung   | MZ-5EA2000-0D3     | 200 GB | 4       | 1475  | 0     | 4.04   |
| SanDisk   | PU1000064GBATSSD   | 64 GB  | 1       | 1449  | 0     | 3.97   |
| SanDisk   | SDSSDXP480G        | 480 GB | 2       | 1447  | 0     | 3.97   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 2       | 1428  | 0     | 3.91   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 1       | 1425  | 0     | 3.91   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 2       | 1416  | 0     | 3.88   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 1       | 1408  | 0     | 3.86   |
| Intel     | SSDSC2CT180A4      | 180 GB | 3       | 1870  | 1     | 3.82   |
| Samsung   | SSD PB22-JS3 2.5"  | 128 GB | 1       | 1365  | 0     | 3.74   |
| SanDisk   | SSD U100           | 8 GB   | 1       | 1365  | 0     | 3.74   |
| Samsung   | SSD 840 Series     | 120 GB | 5       | 1364  | 0     | 3.74   |
| Plextor   | PX-512M5Pro        | 512 GB | 1       | 1361  | 0     | 3.73   |
| AMD       | R3SL120G           | 120 GB | 2       | 1341  | 0     | 3.68   |
| Samsung   | SSD 840 Series     | 250 GB | 2       | 1328  | 0     | 3.64   |
| SuperM... | SSD                | 128 GB | 1       | 1295  | 0     | 3.55   |
| Samsung   | MZ7LM240HCGR-0E003 | 240 GB | 2       | 1295  | 0     | 3.55   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 1       | 1283  | 0     | 3.52   |
| HPE       | MK000480GWCEV      | 480 GB | 2       | 1275  | 0     | 3.49   |
| HPE       | MK000960GWCFA      | 960 GB | 2       | 1275  | 0     | 3.49   |
| Seagate   | XF1230-1A0480      | 480 GB | 2       | 1266  | 0     | 3.47   |
| Kingston  | SUV400S37120G      | 120 GB | 3       | 1257  | 0     | 3.44   |
| Intel     | SSDSC2CT180A3      | 180 GB | 4       | 1740  | 1     | 3.44   |
| Toshiba   | THNSFJ256GDNU      | 256 GB | 1       | 1250  | 0     | 3.43   |
| Toshiba   | THNSNJ128GCSY      | 128 GB | 1       | 1236  | 0     | 3.39   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 4       | 1228  | 0     | 3.37   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 2       | 1224  | 0     | 3.36   |
| Kingston  | SH103S3240G        | 240 GB | 2       | 1224  | 0     | 3.36   |
| SanDisk   | Ultra II           | 960 GB | 2       | 1202  | 0     | 3.29   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 7       | 1185  | 0     | 3.25   |
| Samsung   | SSD RBX Series ... | 64 GB  | 1       | 1182  | 0     | 3.24   |
| Intel     | SSDSC2BB960G7R     | 960 GB | 6       | 1177  | 0     | 3.23   |
| SuperM... | SSD                | 16 GB  | 1       | 1176  | 0     | 3.22   |
| Dell      | SSDSCKJB120G7R     | 120 GB | 2       | 1173  | 0     | 3.22   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 1154  | 0     | 3.16   |
| Intel     | SSDSC2BX400G4      | 400 GB | 1       | 1145  | 0     | 3.14   |
| Samsung   | SSD 830 Series     | 128 GB | 5       | 1144  | 0     | 3.13   |
| Kingston  | SMS200S360G        | 64 GB  | 5       | 1297  | 1     | 3.13   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 1       | 1131  | 0     | 3.10   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 2       | 1117  | 0     | 3.06   |
| ADATA     | SP600              | 32 GB  | 2       | 1097  | 0     | 3.01   |
| HP        | VK0480GECQP        | 480 GB | 1       | 1083  | 0     | 2.97   |
| OCZ       | VERTEX3            | 240 GB | 1       | 1081  | 0     | 2.96   |
| OCZ       | VERTEX3            | 64 GB  | 4       | 1591  | 8     | 2.96   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 1       | 2157  | 1     | 2.96   |
| SanDisk   | SD7SF6S512G1122    | 512 GB | 1       | 1073  | 0     | 2.94   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 1       | 1067  | 0     | 2.92   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 1       | 1060  | 0     | 2.91   |
| Kingston  | SKC400S37512G      | 512 GB | 2       | 1059  | 0     | 2.90   |
| Crucial   | FCCT128M4SSD1      | 128 GB | 2       | 1042  | 0     | 2.86   |
| Goodram   | SSD                | 240 GB | 3       | 1037  | 0     | 2.84   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 3       | 1033  | 0     | 2.83   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 1       | 1021  | 0     | 2.80   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 1       | 1012  | 0     | 2.77   |
| ADATA     | SX930              | 240 GB | 1       | 1001  | 0     | 2.74   |
| Samsung   | SSD 840 EVO        | 500 GB | 4       | 1138  | 209   | 2.74   |
| Kingston  | SVP200S37A60G      | 64 GB  | 2       | 999   | 0     | 2.74   |
| Samsung   | SSD 850 EVO        | 120 GB | 5       | 997   | 0     | 2.73   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 4       | 987   | 0     | 2.71   |
| Intel     | SSDMCEAW080A4      | 80 GB  | 1       | 981   | 0     | 2.69   |
| Crucial   | CT250MX200SSD1     | 250 GB | 5       | 1048  | 1     | 2.68   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 1       | 976   | 0     | 2.67   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 1       | 966   | 0     | 2.65   |
| SanDisk   | SD9SB8W256G1122    | 256 GB | 1       | 961   | 0     | 2.63   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 1       | 959   | 0     | 2.63   |
| SanDisk   | X600 2.5 7MM SATA  | 256 GB | 1       | 947   | 0     | 2.59   |
| Kingston  | SH103S3120G        | 120 GB | 5       | 940   | 0     | 2.58   |
| Crucial   | CT240M500SSD3      | 240 GB | 1       | 917   | 0     | 2.51   |
| OCZ       | ARC100             | 240 GB | 2       | 916   | 0     | 2.51   |
| ADATA     | SP900              | 64 GB  | 1       | 895   | 0     | 2.45   |
| Seagate   | ST100FN0021        | 100 GB | 1       | 1781  | 1     | 2.44   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 1       | 888   | 0     | 2.44   |
| HPE       | MK000240GWEZF      | 240 GB | 2       | 882   | 0     | 2.42   |
| Samsung   | SSD 750 EVO        | 250 GB | 6       | 864   | 0     | 2.37   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 1       | 862   | 0     | 2.36   |
| Intel     | SSDSC2CW240A3      | 240 GB | 1       | 854   | 0     | 2.34   |
| ADATA     | IM2S3134N-064GM    | 64 GB  | 1       | 851   | 0     | 2.33   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 2       | 848   | 0     | 2.33   |
| Corsair   | Force 3 SSD        | 180 GB | 1       | 2530  | 2     | 2.31   |
| ADATA     | SP900              | 128 GB | 2       | 840   | 0     | 2.30   |
| OCZ       | VERTEX2            | 120 GB | 1       | 835   | 0     | 2.29   |
| Intel     | SSDSC2BP240G4      | 240 GB | 1       | 835   | 0     | 2.29   |
| PNY       | CS1311 240GB SSD   | 240 GB | 3       | 833   | 0     | 2.28   |
| Kingston  | SM2280S3120G       | 120 GB | 1       | 833   | 0     | 2.28   |
| Kingston  | SS200S330G         | 32 GB  | 2       | 833   | 0     | 2.28   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 4       | 826   | 0     | 2.26   |
| Toshiba   | THNSNC128GBSJ      | 128 GB | 1       | 826   | 0     | 2.26   |
| Intel     | SSDSC2BB480G7      | 480 GB | 3       | 940   | 1     | 2.26   |
| ADATA     | SP600              | 128 GB | 1       | 813   | 0     | 2.23   |
| Samsung   | SSD 830 Series     | 64 GB  | 2       | 812   | 0     | 2.23   |
| Kingston  | SUV300S37A240G     | 240 GB | 1       | 807   | 0     | 2.21   |
| Corsair   | Force GS           | 180 GB | 1       | 807   | 0     | 2.21   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 3       | 804   | 0     | 2.20   |
| Plextor   | PH6-CE120-G        | 120 GB | 1       | 804   | 0     | 2.20   |
| ADATA     | SSD S599           | 40 GB  | 1       | 802   | 0     | 2.20   |
| SanDisk   | X300 MSATA         | 256 GB | 1       | 800   | 0     | 2.19   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 2       | 798   | 0     | 2.19   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 4       | 795   | 0     | 2.18   |
| Samsung   | SSD 850 EVO        | 250 GB | 53      | 792   | 0     | 2.17   |
| Plextor   | PX-64G5Le          | 64 GB  | 1       | 791   | 0     | 2.17   |
| Intel     | SSDSC2BW120A3      | 120 GB | 1       | 790   | 0     | 2.17   |
| Crucial   | CT960M500SSD1      | 960 GB | 2       | 787   | 0     | 2.16   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 3       | 787   | 0     | 2.16   |
| Samsung   | SSD 850 PRO        | 512 GB | 12      | 782   | 0     | 2.14   |
| Samsung   | MZNLN128HCGR-000L1 | 128 GB | 1       | 781   | 0     | 2.14   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 4       | 778   | 0     | 2.13   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 6       | 775   | 0     | 2.12   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 2       | 1071  | 163   | 2.12   |
| Innodisk  | DEMSR- 16GB mSA... | 16 GB  | 1       | 768   | 0     | 2.11   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 4       | 768   | 0     | 2.11   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 1       | 765   | 0     | 2.10   |
| MyDigi... | SB2                | 128 GB | 1       | 763   | 0     | 2.09   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 1       | 762   | 0     | 2.09   |
| SanDisk   | Ultra II           | 480 GB | 3       | 762   | 0     | 2.09   |
| Apple     | SSD TS256C         | 256 GB | 1       | 752   | 0     | 2.06   |
| Samsung   | SSD CM871 2.5 7mm  | 128 GB | 1       | 750   | 0     | 2.06   |
| SanDisk   | SSD U100           | 24 GB  | 2       | 745   | 0     | 2.04   |
| Samsung   | SSD 840 PRO Series | 256 GB | 9       | 963   | 1     | 2.04   |
| Samsung   | SSD 850 EVO        | 2 TB   | 1       | 742   | 0     | 2.03   |
| Phison    | SATA SSD           | 120 GB | 4       | 741   | 0     | 2.03   |
| Mushkin   | MKNSSDTR1TB-3DL    | 1 TB   | 1       | 734   | 0     | 2.01   |
| Samsung   | SSD 830 Series     | 256 GB | 2       | 731   | 0     | 2.00   |
| Samsung   | SSD 840 EVO        | 250 GB | 16      | 725   | 0     | 1.99   |
| Intel     | SSDSC2BW240H6      | 240 GB | 2       | 723   | 0     | 1.98   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 1       | 721   | 0     | 1.98   |
| Kingston  | SV300S37A240G      | 240 GB | 2       | 720   | 0     | 1.97   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 6       | 719   | 0     | 1.97   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 1       | 709   | 0     | 1.94   |
| Toshiba   | TL100              | 240 GB | 1       | 707   | 0     | 1.94   |
| Intel     | SSDSCKHW240A4      | 240 GB | 1       | 695   | 0     | 1.90   |
| Kingston  | SUV400S37240G      | 240 GB | 4       | 693   | 0     | 1.90   |
| Toshiba   | THNSNF256GMCS      | 256 GB | 1       | 690   | 0     | 1.89   |
| Kingston  | SHFS37A240G        | 240 GB | 3       | 689   | 0     | 1.89   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 1       | 683   | 0     | 1.87   |
| ADATA     | SP600              | 64 GB  | 2       | 683   | 0     | 1.87   |
| Dogfish   | SSD 30G            | 32 GB  | 1       | 676   | 0     | 1.85   |
| Samsung   | SSD 850 EVO        | 1 TB   | 8       | 875   | 1     | 1.84   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 2       | 669   | 0     | 1.83   |
| Apple     | SSD TS128C         | 121 GB | 2       | 667   | 0     | 1.83   |
| Intel     | SSDSC2BB150G7      | 150 GB | 4       | 793   | 1     | 1.81   |
| Kingston  | SV300S37A120G      | 120 GB | 19      | 866   | 2     | 1.81   |
| SanDisk   | SDSSDA120G         | 120 GB | 11      | 659   | 0     | 1.81   |
| OWC       | Mercury Extreme... | 240 GB | 1       | 657   | 0     | 1.80   |
| SPCC      | SSD                | 64 GB  | 3       | 655   | 0     | 1.80   |
| SanDisk   | SD6SB1M064G1022I   | 64 GB  | 3       | 653   | 0     | 1.79   |
| Kingston  | SMSM150S324G2      | 24 GB  | 1       | 650   | 0     | 1.78   |
| Samsung   | SG9MSM6D024GPM00   | 22 GB  | 1       | 649   | 0     | 1.78   |
| OWC       | Mercury Electra... | 240 GB | 2       | 649   | 0     | 1.78   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 2       | 646   | 0     | 1.77   |
| OCZ       | VERTEX3            | 120 GB | 5       | 1216  | 34    | 1.76   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 6       | 2371  | 7     | 1.76   |
| Samsung   | SSD 850 PRO        | 256 GB | 9       | 642   | 0     | 1.76   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 1       | 642   | 0     | 1.76   |
| Corsair   | Force 3 SSD        | 64 GB  | 2       | 638   | 0     | 1.75   |
| Samsung   | SSD 850 EVO        | 500 GB | 24      | 665   | 1     | 1.72   |
| Innodisk  | Corp. mSATA 3SE... | 2 GB   | 1       | 617   | 0     | 1.69   |
| Intel     | SSDSC2CT120A3      | 120 GB | 2       | 981   | 2     | 1.68   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 1       | 612   | 0     | 1.68   |
| SanDisk   | SDSSDP128G         | 128 GB | 4       | 612   | 0     | 1.68   |
| Kingston  | SHFS37A120G        | 120 GB | 3       | 611   | 0     | 1.68   |
| Intel     | SSDSA2CW160G3      | 160 GB | 1       | 610   | 0     | 1.67   |
| SanDisk   | SDSSDXP120G        | 120 GB | 1       | 608   | 0     | 1.67   |
| Intel     | SSDSC2BW180A4      | 180 GB | 1       | 606   | 0     | 1.66   |
| Team      | TEAML5Lite3D1T     | 1 TB   | 1       | 596   | 0     | 1.63   |
| Micron    | MTFDDAK120MBB-1... | 120 GB | 1       | 590   | 0     | 1.62   |
| SanDisk   | SDSA6GM-016G-1006  | 16 GB  | 1       | 589   | 0     | 1.62   |
| Intel     | SSDSC2BW120A4      | 120 GB | 4       | 578   | 0     | 1.59   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 4       | 577   | 0     | 1.58   |
| Kingston  | SUV400S37480G      | 480 GB | 1       | 566   | 0     | 1.55   |
| Samsung   | MZNLN256HAJQ-000H1 | 256 GB | 1       | 558   | 0     | 1.53   |
| Crucial   | CT256MX100SSD1     | 256 GB | 6       | 551   | 0     | 1.51   |
| SanDisk   | SSD U100           | 16 GB  | 3       | 548   | 0     | 1.50   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 1       | 544   | 0     | 1.49   |
| Phison    | SATA SSD           | 16 GB  | 45      | 544   | 0     | 1.49   |
| Samsung   | SSD 750 EVO        | 120 GB | 3       | 540   | 0     | 1.48   |
| Toshiba   | Q300               | 480 GB | 1       | 540   | 0     | 1.48   |
| SanDisk   | SDSSDA240G         | 240 GB | 10      | 531   | 0     | 1.46   |
| Apple     | SSD SM0512F        | 500 GB | 1       | 527   | 0     | 1.44   |
| Apple     | SSD SM256C         | 256 GB | 1       | 520   | 0     | 1.43   |
| Phison    | SATA SSD           | 8 GB   | 1       | 508   | 0     | 1.39   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 1       | 508   | 0     | 1.39   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 1       | 505   | 0     | 1.38   |
| Toshiba   | A100               | 240 GB | 1       | 503   | 0     | 1.38   |
| Kingston  | SV300S37A480G      | 480 GB | 1       | 501   | 0     | 1.37   |
| V-GeN     | V-GEN08AS19FS120IT | 120 GB | 1       | 500   | 0     | 1.37   |
| PNY       | CS1311 120GB SSD   | 120 GB | 1       | 497   | 0     | 1.36   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 3       | 496   | 0     | 1.36   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 2       | 487   | 0     | 1.34   |
| Plextor   | PX-128M7VC         | 128 GB | 1       | 483   | 0     | 1.32   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 1       | 483   | 0     | 1.32   |
| Samsung   | SSD 860 EVO        | 2 TB   | 3       | 480   | 0     | 1.32   |
| Intel     | SSDMCEAW120A4      | 120 GB | 3       | 476   | 0     | 1.30   |
| Samsung   | SSD 750 EVO        | 500 GB | 2       | 471   | 0     | 1.29   |
| KingSpec  | KSD-SA25.7-016MJ   | 16 GB  | 1       | 471   | 0     | 1.29   |
| China     | SATA SSD           | 120 GB | 2       | 471   | 0     | 1.29   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 2       | 470   | 0     | 1.29   |
| Intel     | SSDSC2BA400G4      | 400 GB | 1       | 465   | 0     | 1.28   |
| CWDISK    | SSD                | 32 GB  | 1       | 455   | 0     | 1.25   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 5       | 1692  | 610   | 1.24   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 1       | 451   | 0     | 1.24   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 3       | 495   | 5     | 1.23   |
| SanDisk   | SDSSDH3 1T02       | 1 TB   | 1       | 449   | 0     | 1.23   |
| SanDisk   | SDSSDHII120G       | 120 GB | 3       | 448   | 0     | 1.23   |
| Micron    | 5200_MTFDDAK1T9TDN | 1.9 TB | 2       | 446   | 0     | 1.22   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 3       | 446   | 0     | 1.22   |
| AEGO      | SSD                | 120 GB | 1       | 445   | 0     | 1.22   |
| Samsung   | SSD PM830 FDE 2... | 256 GB | 1       | 440   | 0     | 1.21   |
| Intenso   | lntenso SSD Sat... | 120 GB | 1       | 438   | 0     | 1.20   |
| Phison    | SATA SSD           | 128 GB | 5       | 438   | 0     | 1.20   |
| ADATA     | SU750              | 1 TB   | 1       | 435   | 0     | 1.19   |
| SanDisk   | Ultra II           | 240 GB | 2       | 432   | 0     | 1.19   |
| Kingston  | SMS200S330G        | 32 GB  | 6       | 884   | 3     | 1.18   |
| Kingston  | SV300S37A60G       | 64 GB  | 7       | 875   | 116   | 1.18   |
| TCSUNBOW  | M1                 | 32 GB  | 3       | 429   | 0     | 1.18   |
| Crucial   | CT480BX300SSD1     | 480 GB | 1       | 429   | 0     | 1.18   |
| SanDisk   | SSD U110           | 16 GB  | 7       | 426   | 0     | 1.17   |
| Vaseky    | V800-60G           | 64 GB  | 1       | 426   | 0     | 1.17   |
| SK hynix  | SC300 M.2 2280     | 128 GB | 1       | 425   | 0     | 1.17   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 1       | 424   | 0     | 1.16   |
| SPCC      | SSD                | 240 GB | 1       | 422   | 0     | 1.16   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 1       | 422   | 0     | 1.16   |
| SanDisk   | SDSSDH3512G        | 512 GB | 1       | 415   | 0     | 1.14   |
| ADATA     | SSD S510           | 64 GB  | 1       | 414   | 0     | 1.14   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 2       | 410   | 0     | 1.12   |
| SPCC      | SSD                | 1 TB   | 18      | 405   | 0     | 1.11   |
| Intel     | SSDSC2KW256G8      | 256 GB | 4       | 403   | 0     | 1.10   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 1       | 400   | 0     | 1.10   |
| Hoodisk   | SSD                | 32 GB  | 20      | 397   | 0     | 1.09   |
| Samsung   | MZMTD256HAGM-000L1 | 256 GB | 1       | 391   | 0     | 1.07   |
| Kingston  | SMS100S264G        | 64 GB  | 1       | 389   | 0     | 1.07   |
| Samsung   | SSD 840 EVO        | 1 TB   | 4       | 385   | 0     | 1.06   |
| KingSpec  | P3-120             | 120 GB | 1       | 385   | 0     | 1.06   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 1       | 385   | 0     | 1.06   |
| SanDisk   | SD9SB8W128G1122    | 128 GB | 1       | 381   | 0     | 1.05   |
| OCZ       | VECTOR150          | 120 GB | 1       | 758   | 1     | 1.04   |
| KingDian  | S280               | 240 GB | 1       | 378   | 0     | 1.04   |
| Hoodisk   | SSD                | 16 GB  | 9       | 375   | 0     | 1.03   |
| SanDisk   | SDSSDHII240G       | 240 GB | 1       | 374   | 0     | 1.03   |
| OCZ       | TRION150           | 480 GB | 1       | 373   | 0     | 1.02   |
| Transcend | TS128GSSD370S      | 128 GB | 3       | 372   | 0     | 1.02   |
| AVEXIR    | E100 SERIES -      | 120 GB | 1       | 365   | 0     | 1.00   |
| SanDisk   | SDSSDH3500G        | 500 GB | 1       | 365   | 0     | 1.00   |
| Apacer    | APSDM050GM1AN-T... | 54 GB  | 1       | 364   | 0     | 1.00   |
| SanDisk   | SDSSDHII960G       | 960 GB | 2       | 364   | 0     | 1.00   |
| Transcend | TS128GMTS400       | 128 GB | 2       | 360   | 0     | 0.99   |
| Zheino    | CHN-mSATAM3-256    | 256 GB | 2       | 360   | 0     | 0.99   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 3       | 358   | 0     | 0.98   |
| Samsung   | MZ7KM960HAHP-0Z005 | 960 GB | 1       | 356   | 0     | 0.98   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 5       | 368   | 1     | 0.97   |
| Kingston  | SVP100S2512G       | 512 GB | 1       | 353   | 0     | 0.97   |
| Kingston  | RBUSNS8180S3128GI  | 128 GB | 1       | 351   | 0     | 0.96   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 2       | 351   | 0     | 0.96   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 2       | 350   | 0     | 0.96   |
| SanDisk   | SDSSDP256G         | 256 GB | 2       | 349   | 0     | 0.96   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 1       | 349   | 0     | 0.96   |
| Intenso   | SSD Sata III       | 120 GB | 5       | 341   | 0     | 0.94   |
| Crucial   | CT525MX300SSD1     | 528 GB | 9       | 522   | 2     | 0.93   |
| Samsung   | MZ7LF192HCGS-000L1 | 192 GB | 1       | 335   | 0     | 0.92   |
| Lite-On   | IT LCS-256L9S      | 256 GB | 1       | 334   | 0     | 0.92   |
| Samsung   | SSD 860 PRO        | 1 TB   | 3       | 333   | 0     | 0.91   |
| Mushkin   | MKNSSDAT120GB-V    | 120 GB | 1       | 332   | 0     | 0.91   |
| SanDisk   | SD6SB1M-032G-1006  | 32 GB  | 1       | 331   | 0     | 0.91   |
| Smartbuy  | SSD                | 64 GB  | 1       | 327   | 0     | 0.90   |
| Kingston  | SMS200S3120G       | 120 GB | 6       | 819   | 3     | 0.89   |
| Kingston  | SUV500M8120G       | 120 GB | 1       | 320   | 0     | 0.88   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 6       | 316   | 0     | 0.87   |
| OCZ       | AGILITY3           | 240 GB | 1       | 1553  | 4     | 0.85   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 2       | 308   | 0     | 0.85   |
| Samsung   | SSD 860 EVO        | 500 GB | 31      | 306   | 0     | 0.84   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 1       | 306   | 0     | 0.84   |
| Hyundai   | 120GB SSD          | 120 GB | 1       | 306   | 0     | 0.84   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 1       | 303   | 0     | 0.83   |
| KingDian  | S400               | 120 GB | 1       | 303   | 0     | 0.83   |
| Transcend | 3E128-TS2-550B01   | 100 GB | 4       | 404   | 257   | 0.83   |
| Phison    | SATA SSD           | 32 GB  | 7       | 301   | 0     | 0.83   |
| SanDisk   | SDSSDP064G         | 64 GB  | 2       | 300   | 0     | 0.82   |
| Crucial   | CT500MX500SSD4     | 500 GB | 3       | 297   | 0     | 0.81   |
| OCZ       | VERTEX4            | 128 GB | 1       | 1188  | 3     | 0.81   |
| Intel     | SSDSC2CT240A3      | 240 GB | 1       | 2370  | 7     | 0.81   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 3       | 1438  | 29    | 0.81   |
| SanDisk   | SSD U110           | 24 GB  | 1       | 295   | 0     | 0.81   |
| Intenso   | SSD                | 128 GB | 1       | 295   | 0     | 0.81   |
| WDC       | WDS200T2B0A        | 2 TB   | 1       | 588   | 1     | 0.81   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 1       | 291   | 0     | 0.80   |
| WDC       | WDBNCE2500PNC      | 250 GB | 1       | 287   | 0     | 0.79   |
| Crucial   | CT250MX500SSD4     | 250 GB | 2       | 285   | 0     | 0.78   |
| SanDisk   | SSD U100           | 128 GB | 1       | 282   | 0     | 0.77   |
| SMART     | SSD XceedValue2... | 32 GB  | 1       | 280   | 0     | 0.77   |
| HP        | SSD S700 Pro       | 512 GB | 2       | 280   | 0     | 0.77   |
| PNY       | CS900 120GB SSD    | 120 GB | 10      | 279   | 0     | 0.76   |
| Intel     | SSDSC2BB120G4      | 120 GB | 3       | 279   | 0     | 0.76   |
| SanDisk   | SD9SN8W128G1002    | 128 GB | 1       | 278   | 0     | 0.76   |
| Transcend | TS64GMTS400S       | 64 GB  | 2       | 271   | 0     | 0.74   |
| Apacer    | 16GB SATA Flash... | 16 GB  | 5       | 412   | 3     | 0.74   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 7       | 268   | 0     | 0.74   |
| SanDisk   | SD6SB2M512G1022I   | 512 GB | 1       | 536   | 1     | 0.74   |
| SK hynix  | HFS128G32MND-2200A | 128 GB | 1       | 798   | 2     | 0.73   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 1       | 264   | 0     | 0.72   |
| Crucial   | CT120M500SSD1      | 120 GB | 3       | 261   | 0     | 0.72   |
| Toshiba   | TR200              | 240 GB | 4       | 257   | 0     | 0.70   |
| PNY       | CS900 250GB SSD    | 250 GB | 1       | 256   | 0     | 0.70   |
| SanDisk   | SSD PLUS           | 120 GB | 16      | 256   | 0     | 0.70   |
| SanDisk   | SDSSDH3 500G       | 500 GB | 2       | 254   | 0     | 0.70   |
| OWC       | Mercury Electra... | 1 TB   | 5       | 252   | 0     | 0.69   |
| Apple     | SSD SM1024G        | 1 TB   | 1       | 251   | 0     | 0.69   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 3       | 250   | 0     | 0.69   |
| BIWIN     | SSD                | 256 GB | 1       | 249   | 0     | 0.68   |
| Apacer    | 32GB SATA Flash... | 32 GB  | 3       | 784   | 4     | 0.68   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 2       | 247   | 0     | 0.68   |
| SPCC      | SSD                | 512 GB | 4       | 247   | 0     | 0.68   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 1       | 245   | 0     | 0.67   |
| Patriot   | Burst              | 240 GB | 4       | 245   | 0     | 0.67   |
| Indilinx  | IND-S3MP-256G      | 256 GB | 1       | 243   | 0     | 0.67   |
| Plextor   | PX-128M5S          | 128 GB | 1       | 1216  | 4     | 0.67   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 1       | 239   | 0     | 0.66   |
| Samsung   | SSD 840 Series     | 500 GB | 1       | 238   | 0     | 0.65   |
| Hoodisk   | SSD                | 128 GB | 18      | 238   | 0     | 0.65   |
| Kingston  | SUV500MS120G       | 120 GB | 32      | 238   | 0     | 0.65   |
| Samsung   | MZ7LN256HMJP-000L7 | 256 GB | 1       | 234   | 0     | 0.64   |
| Hoodisk   | SSD                | 64 GB  | 24      | 234   | 0     | 0.64   |
| Transcend | TS64GSSD340        | 64 GB  | 1       | 230   | 0     | 0.63   |
| Plextor   | PX-256M8VG         | 256 GB | 1       | 230   | 0     | 0.63   |
| Faspeed   | K5M-32G            | 32 GB  | 1       | 230   | 0     | 0.63   |
| SanDisk   | SD8TN8U256G1001    | 256 GB | 1       | 225   | 0     | 0.62   |
| Intel     | SSDSC2BP480G4      | 480 GB | 1       | 224   | 0     | 0.62   |
| Samsung   | MZHPV512HDGL-000L1 | 512 GB | 1       | 222   | 0     | 0.61   |
| Corsair   | CSSD-V64GB2        | 64 GB  | 1       | 221   | 0     | 0.61   |
| Kingston  | SA400S37240G       | 240 GB | 43      | 219   | 0     | 0.60   |
| Samsung   | MZ7TY128HDHP-00000 | 128 GB | 1       | 218   | 0     | 0.60   |
| Corsair   | Force LS SSD       | 64 GB  | 2       | 217   | 0     | 0.60   |
| Transcend | TS16GMTS400        | 16 GB  | 1       | 217   | 0     | 0.60   |
| Intel     | SSDSA2M120G2GC     | 120 GB | 1       | 1086  | 4     | 0.60   |
| Samsung   | SSD 860 EVO        | 250 GB | 23      | 217   | 0     | 0.59   |
| China     | SSD                | 64 GB  | 2       | 214   | 0     | 0.59   |
| Kingston  | SA400S37120G       | 120 GB | 33      | 214   | 0     | 0.59   |
| Crucial   | CT275MX300SSD4     | 275 GB | 1       | 213   | 0     | 0.59   |
| Transcend | TS512GSSD370       | 512 GB | 2       | 212   | 0     | 0.58   |
| Samsung   | SSD 860 EVO        | 1 TB   | 13      | 211   | 0     | 0.58   |
| PNY       | CS900 240GB SSD    | 240 GB | 9       | 209   | 0     | 0.58   |
| HP        | SSD S700 Pro       | 256 GB | 1       | 207   | 0     | 0.57   |
| Apple     | SSD SD0128F        | 121 GB | 2       | 370   | 1     | 0.57   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 1       | 207   | 0     | 0.57   |
| OCZ       | VERTEX4            | 64 GB  | 1       | 206   | 0     | 0.57   |
| Kingston  | SUV500240G         | 240 GB | 3       | 205   | 0     | 0.56   |
| SanDisk   | SD8TN8U512G1001    | 512 GB | 1       | 204   | 0     | 0.56   |
| SanDisk   | X400 M.2 2280      | 512 GB | 1       | 204   | 0     | 0.56   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 6       | 203   | 0     | 0.56   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 5       | 300   | 2     | 0.56   |
| WDC       | WDS100T1R0A-68A4W0 | 1 TB   | 1       | 202   | 0     | 0.55   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 1       | 200   | 0     | 0.55   |
| HP        | SSD S700           | 1 TB   | 1       | 198   | 0     | 0.54   |
| SPCC      | SPCCSolidStateDisk | 256 GB | 2       | 197   | 0     | 0.54   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 1       | 196   | 0     | 0.54   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 1       | 196   | 0     | 0.54   |
| Transcend | TS32GSSD340K       | 32 GB  | 1       | 196   | 0     | 0.54   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 2       | 1170  | 6     | 0.54   |
| Crucial   | CT120BX500SSD1     | 120 GB | 25      | 195   | 0     | 0.54   |
| Intel     | SSDSC2BW480A4      | 480 GB | 1       | 976   | 4     | 0.53   |
| Intel     | SSDSC2BF180A4H     | 180 GB | 1       | 195   | 0     | 0.53   |
| SanDisk   | SSD PLUS           | 240 GB | 9       | 281   | 5     | 0.53   |
| Intel     | SSDSC2KW128G8      | 128 GB | 2       | 193   | 0     | 0.53   |
| Crucial   | CT500MX200SSD1     | 500 GB | 3       | 191   | 0     | 0.52   |
| Pioneer   | APS-SL3N-128       | 128 GB | 1       | 189   | 0     | 0.52   |
| Apacer    | 128GB SATA Flas... | 128 GB | 1       | 187   | 0     | 0.51   |
| Innodisk  | Corp. DRPS-16GJ... | 16 GB  | 1       | 187   | 0     | 0.51   |
| MyDigi... | SC2 M2 SSD         | 120 GB | 1       | 186   | 0     | 0.51   |
| Goodram   | SSD                | 120 GB | 2       | 186   | 0     | 0.51   |
| Toshiba   | Q300               | 240 GB | 2       | 186   | 0     | 0.51   |
| Samsung   | SSD 860 PRO        | 512 GB | 2       | 185   | 0     | 0.51   |
| Samsung   | SSD 860 PRO        | 256 GB | 10      | 185   | 0     | 0.51   |
| AMD       | R5SL240G           | 240 GB | 1       | 183   | 0     | 0.50   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 2       | 183   | 0     | 0.50   |
| China     | SSD 128G           | 128 GB | 1       | 181   | 0     | 0.50   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 4       | 181   | 0     | 0.50   |
| Kingston  | SM2280S3G2240G     | 240 GB | 1       | 181   | 0     | 0.50   |
| Samsung   | MZ7LH1T9HMLT0D3    | 1.9 TB | 2       | 180   | 0     | 0.50   |
| Transcend | TS64GSSD370        | 64 GB  | 2       | 180   | 0     | 0.49   |
| Intel     | SSDSA2SH064G1GC    | 64 GB  | 1       | 179   | 0     | 0.49   |
| China     | DHMSR64GD81BC1QC   | 54 GB  | 2       | 177   | 0     | 0.49   |
| KingDian  | S280-240GB         | 240 GB | 1       | 177   | 0     | 0.49   |
| SanDisk   | X400 M.2 2280      | 256 GB | 1       | 176   | 0     | 0.48   |
| Goodram   | IRP_SSDPR_S25B_480 | 480 GB | 1       | 174   | 0     | 0.48   |
| Patriot   | FLARE              | 64 GB  | 1       | 172   | 0     | 0.47   |
| Apple     | SSD SM0512G        | 500 GB | 1       | 170   | 0     | 0.47   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 4       | 169   | 0     | 0.46   |
| SK hynix  | SC311 SATA         | 256 GB | 1       | 168   | 0     | 0.46   |
| Transcend | TS120GMTS420S      | 120 GB | 4       | 167   | 0     | 0.46   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 1       | 166   | 0     | 0.46   |
| SanDisk   | SD5SE2256G1002E    | 256 GB | 1       | 164   | 0     | 0.45   |
| Kston     | SSD                | 32 GB  | 1       | 163   | 0     | 0.45   |
| Kingston  | RBUSNS8180DS3128GH | 128 GB | 1       | 163   | 0     | 0.45   |
| Kingston  | SNV425S2128GB      | 128 GB | 1       | 1457  | 8     | 0.44   |
| EMTEC     | X150               | 240 GB | 1       | 161   | 0     | 0.44   |
| Vaseky    | 128GV800           | 128 GB | 1       | 161   | 0     | 0.44   |
| Samsung   | SSD PM871b M.2 ... | 256 GB | 1       | 158   | 0     | 0.43   |
| Crucial   | CT480BX500SSD1     | 480 GB | 1       | 157   | 0     | 0.43   |
| Lite-On   | CV3-CE128-HP       | 128 GB | 1       | 157   | 0     | 0.43   |
| WDC       | WDS500G2B0B-00YS70 | 500 GB | 4       | 157   | 0     | 0.43   |
| China     | 40GB SATA Flash... | 40 GB  | 1       | 156   | 0     | 0.43   |
| Plextor   | PX-64M5M           | 64 GB  | 1       | 154   | 0     | 0.42   |
| SK hynix  | SC311 SATA         | 512 GB | 1       | 153   | 0     | 0.42   |
| Intel     | SSDSCKGF180A4L     | 180 GB | 1       | 152   | 0     | 0.42   |
| PNY       | CS1311 480GB SSD   | 480 GB | 1       | 152   | 0     | 0.42   |
| Transcend | TS256GSSD230S      | 256 GB | 1       | 147   | 0     | 0.40   |
| Patriot   | Burst              | 120 GB | 4       | 146   | 0     | 0.40   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 11      | 145   | 0     | 0.40   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 1       | 144   | 0     | 0.40   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 10      | 144   | 0     | 0.40   |
| Lite-On   | CV8-8E256-11 SATA  | 256 GB | 1       | 143   | 0     | 0.39   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 1       | 139   | 0     | 0.38   |
| KingSpec  | MT-128             | 128 GB | 4       | 139   | 0     | 0.38   |
| Intenso   | SSD Sata III       | 250 GB | 2       | 138   | 0     | 0.38   |
| Hoodisk   | SSD                | 256 GB | 6       | 137   | 0     | 0.38   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 2       | 270   | 1     | 0.37   |
| Samsung   | SSD 860 QVO        | 4 TB   | 2       | 135   | 0     | 0.37   |
| Plextor   | PX-256M5M          | 256 GB | 1       | 135   | 0     | 0.37   |
| Corsair   | Force 3 SSD        | 120 GB | 2       | 1339  | 507   | 0.37   |
| SanDisk   | SSD PLUS           | 1 TB   | 3       | 134   | 0     | 0.37   |
| Kingston  | SA400M8240G        | 240 GB | 2       | 133   | 0     | 0.37   |
| Samsung   | MZHPV256HDGL-000L1 | 256 GB | 1       | 131   | 0     | 0.36   |
| Micron    | MTFDDAK512TDL-1... | 512 GB | 1       | 131   | 0     | 0.36   |
| SanDisk   | SD7SN3Q128G1002    | 128 GB | 1       | 131   | 0     | 0.36   |
| Intel     | SSDSC2BF240A5L     | 240 GB | 1       | 130   | 0     | 0.36   |
| Lite-On   | CV8-8E256          | 256 GB | 1       | 130   | 0     | 0.36   |
| ADATA     | SU650              | 120 GB | 9       | 213   | 24    | 0.35   |
| Crucial   | CT250MX500SSD1     | 250 GB | 25      | 126   | 0     | 0.35   |
| WDC       | WDS500G2B0A        | 500 GB | 2       | 125   | 0     | 0.34   |
| Crucial   | CT275MX300SSD1     | 275 GB | 2       | 191   | 6     | 0.34   |
| Apacer    | AS450              | 240 GB | 1       | 123   | 0     | 0.34   |
| Crucial   | CT240BX500SSD1     | 240 GB | 19      | 123   | 0     | 0.34   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 1       | 123   | 0     | 0.34   |
| Lite-On   | LCS-128M6S-HP      | 128 GB | 1       | 123   | 0     | 0.34   |
| HPE       | MK000480GWUGF      | 480 GB | 1       | 369   | 2     | 0.34   |
| Toshiba   | KSG60ZMV256G M.... | 256 GB | 2       | 122   | 0     | 0.34   |
| China     | SH00M120GB         | 120 GB | 2       | 122   | 0     | 0.34   |
| ADATA     | SU650              | 240 GB | 6       | 120   | 0     | 0.33   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 1       | 119   | 0     | 0.33   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 1       | 118   | 0     | 0.32   |
| PNY       | CS900 500GB SSD    | 500 GB | 3       | 117   | 0     | 0.32   |
| SanDisk   | SSD i100           | 24 GB  | 1       | 117   | 0     | 0.32   |
| SanDisk   | SDSSDH3 512G       | 512 GB | 1       | 116   | 0     | 0.32   |
| Verbatim  | Vi500 S3 480GB SSD | 480 GB | 1       | 115   | 0     | 0.32   |
| Toshiba   | THNSNC064GBSJ      | 64 GB  | 1       | 115   | 0     | 0.32   |
| SPCC      | SSD                | 120 GB | 2       | 114   | 0     | 0.31   |
| ADATA     | SU630              | 240 GB | 5       | 166   | 3     | 0.31   |
| Crucial   | CT120BX300SSD1     | 120 GB | 3       | 112   | 0     | 0.31   |
| Crucial   | CT960BX500SSD1     | 960 GB | 2       | 112   | 0     | 0.31   |
| Apacer    | AS330              | 240 GB | 1       | 1006  | 8     | 0.31   |
| KingFast  | SSD                | 256 GB | 1       | 108   | 0     | 0.30   |
| China     | OSSD256GBTSS2      | 256 GB | 1       | 107   | 0     | 0.30   |
| ADATA     | SU800              | 512 GB | 1       | 107   | 0     | 0.30   |
| SK hynix  | SHGS31-250GS-2     | 250 GB | 1       | 106   | 0     | 0.29   |
| China     | BR                 | 64 GB  | 1       | 106   | 0     | 0.29   |
| Samsung   | Portable SSD T5    | 500 GB | 1       | 105   | 0     | 0.29   |
| Intel     | SSDSC2KG480G8R     | 480 GB | 2       | 105   | 0     | 0.29   |
| Phison    | SATA SSD           | 1 TB   | 1       | 105   | 0     | 0.29   |
| Transcend | TS32GMSA370        | 32 GB  | 6       | 105   | 0     | 0.29   |
| Intenso   | SATA III SSD       | 480 GB | 1       | 102   | 0     | 0.28   |
| Transcend | TS64GMTS400SD      | 64 GB  | 1       | 102   | 0     | 0.28   |
| Team      | T253X2512G         | 512 GB | 1       | 101   | 0     | 0.28   |
| ZTC       | SM201-064G         | 64 GB  | 2       | 593   | 13    | 0.28   |
| Samsung   | SSD 860 QVO        | 1 TB   | 7       | 100   | 0     | 0.28   |
| Crucial   | CT128M550SSD3      | 128 GB | 1       | 1705  | 16    | 0.27   |
| Intel     | SSDSC2KG240G8      | 240 GB | 6       | 100   | 0     | 0.27   |
| EMTEC     | X250               | 512 GB | 1       | 98    | 0     | 0.27   |
| SanDisk   | SD9SN8W128G1102    | 128 GB | 1       | 98    | 0     | 0.27   |
| Lite-On   | LCS-128L9S-11 2... | 128 GB | 1       | 98    | 0     | 0.27   |
| China     | 256GB QLC SATA SSD | 256 GB | 1       | 97    | 0     | 0.27   |
| Samsung   | MZNTY256HDHP-000H1 | 256 GB | 1       | 97    | 0     | 0.27   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 8       | 97    | 0     | 0.27   |
| China     | SATA SSD           | 20 GB  | 1       | 96    | 0     | 0.26   |
| BlueRay   | Ultra M8V          | 256 GB | 1       | 95    | 0     | 0.26   |
| Phison    | SATA SSD           | 64 GB  | 3       | 95    | 0     | 0.26   |
| Transcend | TS128GMSA230S      | 128 GB | 9       | 95    | 0     | 0.26   |
| Samsung   | MZMTE128HMGR-000MV | 128 GB | 1       | 94    | 0     | 0.26   |
| Lite-On   | L8H-256V2G         | 256 GB | 1       | 93    | 0     | 0.26   |
| Kingston  | SA400S37480G       | 480 GB | 12      | 101   | 1     | 0.25   |
| Kingston  | SUV500MS240G       | 240 GB | 18      | 91    | 0     | 0.25   |
| Apple     | SSD SM0128G        | 121 GB | 2       | 91    | 0     | 0.25   |
| Intel     | SSDSC2BW240A4      | 240 GB | 1       | 89    | 0     | 0.24   |
| Samsung   | SSD 860 QVO        | 2 TB   | 1       | 88    | 0     | 0.24   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 1       | 88    | 0     | 0.24   |
| OCZ       | AGILITY4           | 128 GB | 1       | 176   | 1     | 0.24   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 1       | 87    | 0     | 0.24   |
| China     | PATA SSD           | 8 GB   | 1       | 87    | 0     | 0.24   |
| Kston     | SSD                | 128 GB | 3       | 165   | 1     | 0.23   |
| ADATA     | IM2S3144-030GK     | 32 GB  | 1       | 85    | 0     | 0.23   |
| China     | SSD                | 120 GB | 2       | 160   | 2     | 0.23   |
| Dogfish   | SSD                | 256 GB | 4       | 84    | 0     | 0.23   |
| Lite-On   | LMT-256L9M-11 M... | 256 GB | 1       | 84    | 0     | 0.23   |
| ADATA     | SU800              | 1 TB   | 1       | 83    | 0     | 0.23   |
| SPCC      | SSD                | 256 GB | 3       | 82    | 0     | 0.23   |
| Transcend | TS32GSSD370        | 32 GB  | 5       | 82    | 0     | 0.23   |
| UDinfo    | M2S                | 120 GB | 3       | 82    | 0     | 0.23   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 19      | 131   | 1     | 0.22   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 1       | 81    | 0     | 0.22   |
| KingFast  | SSD                | 120 GB | 10      | 81    | 91    | 0.22   |
| Transcend | TS64GMSA370        | 64 GB  | 5       | 81    | 0     | 0.22   |
| Crucial   | CT240M500SSD1      | 240 GB | 3       | 224   | 7     | 0.22   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 1       | 76    | 0     | 0.21   |
| Transcend | TS240GMTS420S      | 240 GB | 3       | 75    | 0     | 0.21   |
| SATADOM   | SL 3IE3 V2         | 64 GB  | 4       | 75    | 0     | 0.21   |
| Kingston  | SMSM151S3128GD     | 128 GB | 1       | 598   | 7     | 0.21   |
| SPCC      | SSD                | 128 GB | 6       | 74    | 0     | 0.20   |
| Indilinx  | InM2246S3-128G     | 128 GB | 1       | 71    | 0     | 0.20   |
| Crucial   | CT500MX500SSD1     | 500 GB | 19      | 86    | 1     | 0.20   |
| Micron    | M500_MTFDDAK960MAV | 960 GB | 4       | 1695  | 270   | 0.19   |
| Kingston  | SM2280S3240G       | 240 GB | 1       | 70    | 0     | 0.19   |
| KingSpec  | NT-128             | 128 GB | 2       | 70    | 0     | 0.19   |
| Dogfish   | SSD                | 480 GB | 1       | 210   | 2     | 0.19   |
| SK hynix  | SHGS31-500GS-2     | 500 GB | 1       | 69    | 0     | 0.19   |
| Samsung   | SSD 860 EVO        | 4 TB   | 1       | 68    | 0     | 0.19   |
| Transcend | TS32GHSD370        | 32 GB  | 1       | 67    | 0     | 0.19   |
| Intel     | SSDSCKGF256A5 SATA | 256 GB | 1       | 67    | 0     | 0.19   |
| SanDisk   | WD easystore       | 240 GB | 2       | 66    | 0     | 0.18   |
| Drevo     | X1 SSD             | 64 GB  | 1       | 66    | 0     | 0.18   |
| Drevo     | X1 pro 64G         | 64 GB  | 2       | 66    | 0     | 0.18   |
| Apple     | SSD SM256E         | 256 GB | 2       | 467   | 61    | 0.18   |
| Dogfish   | SSD                | 64 GB  | 3       | 65    | 0     | 0.18   |
| ADATA     | SU800              | 256 GB | 2       | 65    | 0     | 0.18   |
| Plextor   | PX-128M5M          | 128 GB | 1       | 64    | 0     | 0.18   |
| Plextor   | PX-256M5S          | 256 GB | 2       | 64    | 0     | 0.18   |
| SanDisk   | SD8SBAT128G1122    | 128 GB | 1       | 64    | 0     | 0.18   |
| China     | mSATA-64GB SSD     | 64 GB  | 1       | 63    | 0     | 0.17   |
| Micron    | MTFDDAT064MAM-1J2  | 64 GB  | 1       | 62    | 0     | 0.17   |
| Kingston  | SUV500M8240G       | 240 GB | 2       | 62    | 0     | 0.17   |
| Samsung   | MZNTE128HMGR-000SO | 128 GB | 1       | 367   | 5     | 0.17   |
| Dogfish   | SSD                | 512 GB | 3       | 60    | 0     | 0.17   |
| Samsung   | MZMTE1T0HMJH-00000 | 1 TB   | 1       | 59    | 0     | 0.16   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 2       | 59    | 0     | 0.16   |
| SanDisk   | SD6SF1M032G1022    | 32 GB  | 1       | 59    | 0     | 0.16   |
| Samsung   | SSD 870 QVO        | 2 TB   | 2       | 58    | 0     | 0.16   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 1       | 57    | 0     | 0.16   |
| Intel     | SSDSC2MH120A2      | 120 GB | 2       | 57    | 0     | 0.16   |
| SanDisk   | SSD i100           | 32 GB  | 2       | 708   | 6     | 0.16   |
| SanDisk   | SSD U100           | 32 GB  | 1       | 57    | 0     | 0.16   |
| Transcend | TS256GSSD320       | 256 GB | 2       | 170   | 3     | 0.16   |
| Micron    | 5210_MTFDDAK7T6QDE | 7.6 TB | 4       | 55    | 0     | 0.15   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 31      | 53    | 0     | 0.15   |
| KingDian  | S200               | 64 GB  | 3       | 58    | 337   | 0.15   |
| Transcend | TS256GMTS800       | 256 GB | 1       | 53    | 0     | 0.15   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 1       | 53    | 0     | 0.15   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 2       | 53    | 0     | 0.15   |
| Lite-On   | LGT-128M6G         | 128 GB | 1       | 52    | 0     | 0.14   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 4       | 52    | 0     | 0.14   |
| Samsung   | SSD 650            | 120 GB | 1       | 50    | 0     | 0.14   |
| Lenovo    | SSD SL700 120G     | 120 GB | 1       | 50    | 0     | 0.14   |
| Lite-On   | L8H-256V2G-11 M... | 256 GB | 1       | 50    | 0     | 0.14   |
| OCZ       | VERTEX2            | 55 GB  | 1       | 50    | 0     | 0.14   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 4       | 49    | 0     | 0.14   |
| KingDian  | S280               | 120 GB | 1       | 49    | 0     | 0.14   |
| Samsung   | SSD 870 EVO        | 1 TB   | 2       | 49    | 0     | 0.13   |
| ADATA     | SU630              | 480 GB | 1       | 48    | 0     | 0.13   |
| Transcend | TS256GMSA230S      | 256 GB | 3       | 47    | 0     | 0.13   |
| Toshiba   | THNSNJ256GCSY      | 256 GB | 1       | 45    | 0     | 0.12   |
| Transcend | TS128GMTS550T      | 128 GB | 1       | 44    | 0     | 0.12   |
| Intel     | SSDSC2KG480G8      | 480 GB | 5       | 44    | 0     | 0.12   |
| SanDisk   | SD8SN8U-128G-1006  | 128 GB | 1       | 43    | 0     | 0.12   |
| Transcend | TS128GMTS430S      | 128 GB | 3       | 43    | 0     | 0.12   |
| Transcend | TS64GMSA230S       | 64 GB  | 7       | 42    | 0     | 0.12   |
| China     | QST8-512           | 512 GB | 1       | 42    | 0     | 0.12   |
| China     | SSD 64G            | 64 GB  | 1       | 41    | 0     | 0.11   |
| OCZ       | TRION150           | 240 GB | 1       | 40    | 0     | 0.11   |
| SanDisk   | pSSD               | 64 GB  | 5       | 40    | 0     | 0.11   |
| Dogfish   | SSD                | 120 GB | 1       | 121   | 2     | 0.11   |
| KingSpec  | NT-256             | 256 GB | 3       | 39    | 0     | 0.11   |
| Intel     | SSDSC2KW256G8L     | 256 GB | 1       | 39    | 0     | 0.11   |
| Apacer    | AS350              | 256 GB | 2       | 38    | 0     | 0.11   |
| BIWIN     | SSD                | 128 GB | 7       | 37    | 0     | 0.10   |
| WDC       | WDS120G1G0B-00RC30 | 120 GB | 1       | 37    | 0     | 0.10   |
| Samsung   | MZ7LN256HCHP-000F0 | 256 GB | 1       | 37    | 0     | 0.10   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 1       | 37    | 0     | 0.10   |
| Kingston  | SUV400S37 120G     | 120 GB | 1       | 37    | 0     | 0.10   |
| Kston     | SSD                | 64 GB  | 4       | 37    | 0     | 0.10   |
| Samsung   | MZYTE256HMHP-000L2 | 256 GB | 1       | 36    | 0     | 0.10   |
| Micron    | 1100 SATA          | 512 GB | 1       | 36    | 0     | 0.10   |
| SK hynix  | SC308 SATA         | 256 GB | 1       | 182   | 4     | 0.10   |
| FORESEE   | 128GB SSD          | 128 GB | 10      | 36    | 0     | 0.10   |
| ADATA     | SU750              | 256 GB | 1       | 36    | 0     | 0.10   |
| KingSpec  | P3-256             | 256 GB | 1       | 35    | 0     | 0.10   |
| Phison    | SATA SSD           | 240 GB | 1       | 35    | 0     | 0.10   |
| Transcend | TS32GMTS600        | 32 GB  | 1       | 35    | 0     | 0.10   |
| ATP       | SATA III mSATA     | 120 GB | 2       | 34    | 0     | 0.10   |
| SanDisk   | SSD PLUS           | 480 GB | 3       | 51    | 1     | 0.09   |
| MidasF... | SSD                | 256 GB | 1       | 32    | 0     | 0.09   |
| Protectli | 120GB mSATA        | 120 GB | 5       | 32    | 0     | 0.09   |
| OCZ       | VERTEX-TURBO       | 32 GB  | 2       | 298   | 56    | 0.09   |
| Kingston  | HyperX Fury 3D ... | 480 GB | 2       | 31    | 0     | 0.09   |
| Intenso   | SSD Sata III       | 256 GB | 2       | 31    | 0     | 0.09   |
| Toshiba   | TL100              | 120 GB | 1       | 30    | 0     | 0.08   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 1       | 29    | 0     | 0.08   |
| China     | R580               | 64 GB  | 1       | 28    | 0     | 0.08   |
| Kingston  | SKC600256G         | 256 GB | 1       | 28    | 0     | 0.08   |
| SanDisk   | SD9TN8W256G1001    | 256 GB | 1       | 28    | 0     | 0.08   |
| Crucial   | CT480M500SSD1      | 480 GB | 1       | 580   | 20    | 0.08   |
| Apacer    | 8GB SATA Flash ... | 8 GB   | 1       | 1613  | 58    | 0.07   |
| China     | SATA3 64GB SSD     | 64 GB  | 1       | 26    | 0     | 0.07   |
| China     | XJH-128GB          | 128 GB | 1       | 26    | 0     | 0.07   |
| Zheino    | CHN mSATA01M 060   | 64 GB  | 1       | 26    | 0     | 0.07   |
| Apacer    | AS340              | 120 GB | 1       | 25    | 0     | 0.07   |
| SanDisk   | SD5SG2128G1052E    | 128 GB | 1       | 50    | 1     | 0.07   |
| Transcend | TS128GSSD370       | 128 GB | 1       | 25    | 0     | 0.07   |
| Kingston  | SHSS37A240G        | 240 GB | 1       | 25    | 0     | 0.07   |
| OCZ       | AGILITY3           | 64 GB  | 1       | 24    | 0     | 0.07   |
| Samsung   | SSD 870 QVO        | 1 TB   | 2       | 23    | 0     | 0.07   |
| Dogfish   | SSD                | 128 GB | 4       | 23    | 0     | 0.07   |
| China     | CS2246-M512        | 506 GB | 1       | 22    | 0     | 0.06   |
| ATP       | SATA III M.2 2242  | 64 GB  | 1       | 22    | 0     | 0.06   |
| Crucial   | CT512M550SSD1      | 512 GB | 1       | 379   | 16    | 0.06   |
| FORESEE   | 64GB SSD           | 64 GB  | 6       | 22    | 0     | 0.06   |
| Transcend | TS128GMSA370       | 128 GB | 7       | 22    | 0     | 0.06   |
| Transcend | TS512GMSA370       | 512 GB | 1       | 21    | 0     | 0.06   |
| SanDisk   | SSD G5 BICS4       | 1 TB   | 3       | 21    | 0     | 0.06   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 1       | 21    | 0     | 0.06   |
| SanDisk   | SSD i100           | 64 GB  | 1       | 21    | 0     | 0.06   |
| China     | SATA SSD           | 256 GB | 1       | 21    | 0     | 0.06   |
| Kingston  | SUV500MS480G       | 480 GB | 5       | 20    | 0     | 0.06   |
| Intel     | SSDSC2KF256H6L     | 256 GB | 1       | 61    | 2     | 0.06   |
| Transcend | TS512GMTS430S      | 512 GB | 1       | 20    | 0     | 0.06   |
| ORICO     | PH100-128G         | 128 GB | 1       | 19    | 0     | 0.05   |
| China     | Kston128GB         | 128 GB | 1       | 19    | 0     | 0.05   |
| Zheino    | CHN HFmSATA01M 128 | 128 GB | 1       | 18    | 0     | 0.05   |
| MicroD... | 512G SSD           | 512 GB | 1       | 18    | 0     | 0.05   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 4       | 17    | 0     | 0.05   |
| Apple     | A45ACXBA9TA        | 512 GB | 1       | 16    | 0     | 0.04   |
| Samsung   | SSD PM810 2.5" 7mm | 256 GB | 1       | 362   | 24    | 0.04   |
| Samsung   | MZNLN256HAJQ-000L7 | 256 GB | 1       | 14    | 0     | 0.04   |
| Transcend | TS256GMTS400       | 256 GB | 1       | 14    | 0     | 0.04   |
| China     | SH00M240GB         | 240 GB | 1       | 13    | 0     | 0.04   |
| Crucial   | CT128MX100SSD1     | 128 GB | 1       | 235   | 16    | 0.04   |
| Intel     | SSDSC2BF180A5H REF | 180 GB | 1       | 13    | 0     | 0.04   |
| Transcend | TS256GMTS430S      | 256 GB | 4       | 13    | 0     | 0.04   |
| ADATA     | SP610              | 128 GB | 1       | 39    | 2     | 0.04   |
| Samsung   | SSD 850 PRO        | 1 TB   | 1       | 13    | 0     | 0.04   |
| Lite-On   | LMH-128V2M-11 M... | 128 GB | 1       | 13    | 0     | 0.04   |
| PNY       | SSD2SC240G5LC70... | 240 GB | 1       | 13    | 0     | 0.04   |
| KingSpec  | NT-512             | 512 GB | 1       | 12    | 0     | 0.04   |
| Lite-On   | CS1-SP32-11 M.2... | 32 GB  | 1       | 12    | 0     | 0.03   |
| Hikvision | HS-SSD-C100 120G   | 120 GB | 1       | 12    | 0     | 0.03   |
| Lite-On   | LCH-256V2S         | 256 GB | 2       | 12    | 0     | 0.03   |
| KingFast  | SSD                | 512 GB | 2       | 12    | 0     | 0.03   |
| NTC       | SSD                | 120 GB | 1       | 12    | 0     | 0.03   |
| Micron    | 1100 SATA          | 256 GB | 5       | 15    | 1     | 0.03   |
| Samsung   | SSD 870 EVO        | 250 GB | 6       | 11    | 0     | 0.03   |
| Intel     | SSDSC2KB240G8      | 240 GB | 3       | 11    | 0     | 0.03   |
| Protectli | 64GB mSATA         | 64 GB  | 2       | 11    | 0     | 0.03   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 1       | 11    | 0     | 0.03   |
| Intenso   | SSD Sata III       | 240 GB | 1       | 10    | 0     | 0.03   |
| Hikvision | HS-SSD-C100 240G   | 240 GB | 1       | 10    | 0     | 0.03   |
| Intel     | SSDSC2KB960G8      | 960 GB | 1       | 10    | 0     | 0.03   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 1       | 10    | 0     | 0.03   |
| ZTC       | MS001-128G         | 128 GB | 1       | 9     | 0     | 0.03   |
| KingFast  | SSD                | 64 GB  | 1       | 586   | 60    | 0.03   |
| Leven     | JAJS600M512C       | 512 GB | 1       | 9     | 0     | 0.03   |
| ADATA     | SU760              | 1 TB   | 1       | 8     | 0     | 0.02   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 1       | 8     | 0     | 0.02   |
| SK hynix  | HFS128G39TNF-N3A0A | 128 GB | 1       | 8     | 0     | 0.02   |
| Lite-On   | LJH-64V2G-11 M.... | 64 GB  | 1       | 38    | 4     | 0.02   |
| EMTEC     | X150               | 120 GB | 1       | 7     | 0     | 0.02   |
| Intenso   | SSD Sata III       | 128 GB | 2       | 7     | 26    | 0.02   |
| KingSpec  | Q-720              | 720 GB | 1       | 7     | 0     | 0.02   |
| Lexar     | SSD                | 256 GB | 1       | 7     | 0     | 0.02   |
| China     | SSD64G             | 64 GB  | 1       | 64    | 8     | 0.02   |
| SanDisk   | SDSA6MM-008G-1006  | 8 GB   | 1       | 6     | 0     | 0.02   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 2       | 6     | 0     | 0.02   |
| Lexar     | 256GB SSD          | 256 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | SA400M8120G        | 120 GB | 3       | 6     | 0     | 0.02   |
| SK hynix  | SC210 mSATA        | 256 GB | 2       | 248   | 75    | 0.02   |
| SMI       | SSD DISK           | 120 GB | 1       | 519   | 89    | 0.02   |
| Transcend | TS120GMTS820S      | 120 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZNLN256HMHQ-000   | 256 GB | 1       | 5     | 0     | 0.02   |
| Transcend | TS256GMSA452T      | 256 GB | 1       | 5     | 0     | 0.01   |
| HP        | SSD S600           | 240 GB | 1       | 5     | 0     | 0.01   |
| Samsung   | MZMTE128HMGR-000L2 | 128 GB | 1       | 4     | 0     | 0.01   |
| FORESEE   | 32GB SSD           | 32 GB  | 2       | 4     | 0     | 0.01   |
| KingSpec  | KSD-SA25.7-008MJ   | 8 GB   | 1       | 4     | 0     | 0.01   |
| Transcend | TS64GMSA370S       | 64 GB  | 1       | 4     | 0     | 0.01   |
| SanDisk   | SSD P4             | 16 GB  | 1       | 18    | 3     | 0.01   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 1       | 4     | 0     | 0.01   |
| MEMXPRO   | mSATA M3B          | 32 GB  | 2       | 4     | 0     | 0.01   |
| Corsair   | Neutron GTX SSD    | 120 GB | 1       | 678   | 149   | 0.01   |
| ATP       | SATA III 2.5 in... | 120 GB | 1       | 4     | 0     | 0.01   |
| Team      | T253X1240G         | 240 GB | 1       | 4     | 0     | 0.01   |
| Transcend | TS32GSSD370S       | 32 GB  | 5       | 4     | 0     | 0.01   |
| Mushkin   | MKNSSDSR120GB      | 120 GB | 1       | 3     | 0     | 0.01   |
| Apacer    | AS350              | 128 GB | 2       | 3     | 0     | 0.01   |
| Innodisk  | 2.5" SATA SSD 3... | 128 GB | 1       | 3     | 0     | 0.01   |
| Kingston  | OM8P0S3128B-A0     | 128 GB | 1       | 3     | 0     | 0.01   |
| Apacer    | AS220              | 256 GB | 1       | 3     | 0     | 0.01   |
| BIWIN     | SSD                | 64 GB  | 1       | 3     | 0     | 0.01   |
| SanDisk   | SD8SBAT256G1002    | 256 GB | 1       | 3     | 0     | 0.01   |
| Lite-On   | L8H-128V2G         | 128 GB | 1       | 3     | 0     | 0.01   |
| OWC       | Aura               | 960 GB | 1       | 3     | 0     | 0.01   |
| SanDisk   | SD8SNAT-128G-1006  | 128 GB | 1       | 2     | 0     | 0.01   |
| China     | SSD                | 128 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SSD 64G            | 64 GB  | 1       | 2     | 0     | 0.01   |
| SanDisk   | SSD 128G           | 128 GB | 2       | 2     | 0     | 0.01   |
| China     | SATA3 240GB SSD    | 240 GB | 1       | 231   | 97    | 0.01   |
| Protectli | 480GB mSATA        | 480 GB | 1       | 2     | 0     | 0.01   |
| China     | XJH-64GB           | 64 GB  | 1       | 2     | 0     | 0.01   |
| Lite-On   | CV1-8B512          | 512 GB | 1       | 2     | 0     | 0.01   |
| Plextor   | PX-128M6S          | 128 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MMCRE28GFMXP-MVB   | 128 GB | 1       | 2     | 0     | 0.01   |
| China     | W2EM120GDTA-S71... | 120 GB | 1       | 1     | 0     | 0.01   |
| Intel     | SSDSC2BA200G3T     | 200 GB | 3       | 1983  | 1028  | 0.01   |
| Samsung   | MZNLH512HALU-00000 | 512 GB | 1       | 1     | 0     | 0.01   |
| Intel     | SSDSC2BW120H6      | 120 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2CW120A3      | 120 GB | 4       | 1812  | 1018  | 0.00   |
| KingFast  | SSD                | 16 GB  | 1       | 1     | 0     | 0.00   |
| Samsung   | SSD UM410 Serie... | 16 GB  | 1       | 38    | 24    | 0.00   |
| ATP       | SATA III M.2 22... | 240 GB | 1       | 1     | 0     | 0.00   |
| Lexar     | 128GB SSD          | 128 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZ5PA064HMCD-01000 | 64 GB  | 1       | 7     | 4     | 0.00   |
| ADATA     | SP900              | 256 GB | 1       | 606   | 424   | 0.00   |
| Wintec    | 120GB SATA3 SF2... | 120 GB | 1       | 1431  | 1017  | 0.00   |
| China     | MSATA 64GB SSD     | 64 GB  | 1       | 1     | 0     | 0.00   |
| Seagate   | ST-MSATASSD128     | 128 GB | 1       | 1     | 0     | 0.00   |
| Transcend | TS256GMTS952T2     | 256 GB | 4       | 1     | 0     | 0.00   |
| KingSpec  | P3-512-TM          | 512 GB | 1       | 1     | 0     | 0.00   |
| Protectli | 240GB mSATA        | 240 GB | 2       | 1     | 0     | 0.00   |
| Kingston  | SA400S37960G       | 960 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | THNSNK128GCS8 SATA | 128 GB | 1       | 118   | 100   | 0.00   |
| HP        | SSD S700           | 250 GB | 1       | 1     | 0     | 0.00   |
| Protectli | 960GB mSATA        | 960 GB | 1       | 1     | 0     | 0.00   |
| Seagate   | BarraCuda Q1 SS... | 240 GB | 1       | 1     | 0     | 0.00   |
| Dogfish   | SSD                | 32 GB  | 1       | 1     | 0     | 0.00   |
| Lite-On   | LCH-128V2S         | 128 GB | 1       | 1     | 0     | 0.00   |
| OWC       | Mercury EXTREME... | 1.9 TB | 1       | 1     | 0     | 0.00   |
| SanDisk   | SSD i110           | 32 GB  | 2       | 694   | 509   | 0.00   |
| Corsair   | CSSD-F80GBP2       | 90 GB  | 1       | 1022  | 1008  | 0.00   |
| Netac     | W800S 256GB SSD    | 256 GB | 1       | 1     | 0     | 0.00   |
| Micron    | P300-MTFDBAC050SAL | 50 GB  | 1       | 1111  | 1122  | 0.00   |
| China     | M10C               | 128 GB | 1       | 0     | 0     | 0.00   |
| SuperM... | SSD                | 64 GB  | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 2       | 81    | 94    | 0.00   |
| Intel     | SSDSC1BG200G4R     | 200 GB | 2       | 922   | 1028  | 0.00   |
| Intel     | SSDSCKKR128G8      | 128 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD7UB3Q256G1001    | 256 GB | 1       | 84    | 100   | 0.00   |
| Kingston  | RBUSNS8180S3512GJ  | 512 GB | 2       | 0     | 0     | 0.00   |
| FORESEE   | 256GB SSD          | 256 GB | 1       | 0     | 0     | 0.00   |
| Verbatim  | Vi550 S3 SSD       | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | RBU-SNS4151S316GG2 | 16 GB  | 1       | 0     | 0     | 0.00   |
| VisionTek | mSATA              | 120 GB | 2       | 777   | 1016  | 0.00   |
| Toshiba   | THNSNK256GVN8 M... | 256 GB | 1       | 74    | 100   | 0.00   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 1       | 704   | 1023  | 0.00   |
| BAITITON  | BT58SSD07M         | 120 GB | 1       | 0     | 0     | 0.00   |
| China     | GM128              | 128 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | OM8P0S3256B-A0     | 256 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS128GMSA370S      | 128 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 3       | 0     | 0     | 0.00   |
| Goodram   | SSDPR-CX400-256-G2 | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZMTE128HMGR-00007 | 128 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 2       | 0     | 0     | 0.00   |
| ADATA     | SX300              | 128 GB | 2       | 21    | 525   | 0.00   |
| Kingston  | SNS4151S316G       | 16 GB  | 4       | 436   | 1022  | 0.00   |
| Transcend | TS128GMTS600       | 128 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TSA                | 240 GB | 1       | 0     | 0     | 0.00   |
| minisf... | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | ICFS332-016GW      | 16 GB  | 1       | 0     | 0     | 0.00   |
| China     | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KB480G8      | 480 GB | 1       | 0     | 0     | 0.00   |
| Pioneer   | APS-SL3N-256       | 256 GB | 1       | 0     | 0     | 0.00   |
| QUMO      | SSD                | 120 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS16GMSA370        | 16 GB  | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S316GD      | 16 GB  | 1       | 259   | 1022  | 0.00   |
| Transcend | TS32GMTS800        | 32 GB  | 1       | 0     | 0     | 0.00   |
| ATP       | SATA III mSATA SSD | 240 GB | 3       | 0     | 0     | 0.00   |
| Samsung   | SSD 860 PRO        | 2 TB   | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN-mSATAQ3-120    | 120 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | CV8-8E128-HP       | 128 GB | 1       | 146   | 1007  | 0.00   |
| Kingston  | RBU-SNS8350DES3... | 128 GB | 1       | 14    | 99    | 0.00   |
| Intenso   | SSD SATAIII        | 120 GB | 2       | 0     | 1     | 0.00   |
| HP Phison | PSSBN032GA27MC0    | 32 GB  | 1       | 105   | 1067  | 0.00   |
| Intel     | SSDSC2KW120H6      | 120 GB | 1       | 2     | 29    | 0.00   |
| Intenso   | JAJMS600M256G      | 256 GB | 1       | 0     | 0     | 0.00   |
| KLLISRE   | SSD                | 240 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S332G       | 32 GB  | 1       | 79    | 1022  | 0.00   |
| SanDisk   | SD9SN8W-128G-1006  | 128 GB | 1       | 71    | 969   | 0.00   |
| Apacer    | 64GB SATA Flash... | 64 GB  | 1       | 6     | 100   | 0.00   |
| Micron    | MTFDDAK256MAM-1K12 | 256 GB | 1       | 52    | 1010  | 0.00   |
| Micron    | MTFDDAV256TDL-1... | 256 GB | 1       | 45    | 1008  | 0.00   |
| China     | XJH-32GB           | 32 GB  | 1       | 0     | 0     | 0.00   |
| INDMEM    | M.2 2280           | 64 GB  | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KW480H6      | 480 GB | 1       | 39    | 1010  | 0.00   |
| Lexar     | CFAST 64GB CARD    | 64 GB  | 1       | 0     | 6     | 0.00   |
| SMI       | SSD DISK           | 506 GB | 1       | 44    | 2329  | 0.00   |
| Micron    | MTFDDAT128MAM-1J2  | 128 GB | 1       | 28    | 1587  | 0.00   |
| ADATA     | SP550              | 480 GB | 1       | 4     | 1194  | 0.00   |

SSD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| Intel     | 525 Series SSDs        | 2      | 3       | 2005  | 0     | 5.50   |
| Intel     | 320 Series SSDs        | 5      | 14      | 1412  | 0     | 3.87   |
| AMD       | Silicon Motion base... | 1      | 2       | 1341  | 0     | 3.68   |
| SuperM... | Unknown                | 1      | 1       | 1295  | 0     | 3.55   |
| ADATA     | JMicron based SSDs     | 4      | 6       | 1272  | 0     | 3.49   |
| Seagate   | Nytro XF1230 SATA SSD  | 1      | 2       | 1266  | 0     | 3.47   |
| HPE       | Unknown                | 5      | 9       | 1244  | 1     | 3.33   |
| Intel     | Dell Certified Inte... | 2      | 10      | 1198  | 0     | 3.28   |
| Dell      | Certified Intel S35... | 1      | 2       | 1173  | 0     | 3.22   |
| OCZ       | SandForce Driven SSDs  | 10     | 20      | 1425  | 71    | 3.03   |
| Mushkin   | SandForce Driven SSDs  | 2      | 2       | 1096  | 0     | 3.01   |
| Intel     | 330/335 Series SSDs    | 4      | 10      | 1690  | 2     | 2.94   |
| Crucial   | RealSSD m4/C400/P400   | 4      | 12      | 1129  | 86    | 2.93   |
| Crucial   | Unknown                | 1      | 2       | 1042  | 0     | 2.86   |
| ADATA     | JMicron/Maxiotek ba... | 2      | 3       | 1002  | 0     | 2.75   |
| Corsair   | SandForce Driven SSDs  | 9      | 12      | 1296  | 169   | 2.38   |
| Intel     | 730 and DC S35x0/36... | 13     | 24      | 1141  | 129   | 2.35   |
| Toshiba   | HG3 Series             | 1      | 1       | 826   | 0     | 2.26   |
| Micron    | 5100 Pro / 5200 SSDs   | 1      | 4       | 778   | 0     | 2.13   |
| OCZ       | Indilinx Barefoot 3... | 2      | 3       | 863   | 1     | 2.02   |
| Intel     | X18-M/X25-M/X25-V G... | 4      | 10      | 2040  | 6     | 1.98   |
| Toshiba   | HG5 Series             | 1      | 1       | 709   | 0     | 1.94   |
| Toshiba   | HG6 Series SSD         | 4      | 8       | 699   | 0     | 1.92   |
| Goodram   | Phison Driven OEM SSDs | 2      | 5       | 696   | 0     | 1.91   |
| Apple     | JMicron based SSDs     | 2      | 3       | 695   | 0     | 1.91   |
| Kingston  | SSDNow UV400           | 2      | 5       | 668   | 0     | 1.83   |
| Kingston  | SandForce Driven SSDs  | 13     | 62      | 880   | 31    | 1.80   |
| Samsung   | Samsung based SSDs     | 105    | 405     | 684   | 4     | 1.79   |
| ADATA     | SandForce Driven SSDs  | 5      | 6       | 733   | 71    | 1.73   |
| Transcend | JMicron based SSDs     | 2      | 2       | 631   | 0     | 1.73   |
| SanDisk   | SandForce Driven SSDs  | 3      | 22      | 617   | 0     | 1.69   |
| Plextor   | Unknown                | 3      | 3       | 608   | 0     | 1.67   |
| Team      | Silicon Motion base... | 1      | 1       | 596   | 0     | 1.63   |
| SuperM... | Silicon Motion base... | 2      | 2       | 588   | 0     | 1.61   |
| Intel     | 53x and Pro 1500/25... | 10     | 16      | 625   | 1     | 1.58   |
| Innodisk  | Unknown                | 3      | 3       | 524   | 0     | 1.44   |
| V-GeN     | Unknown                | 1      | 1       | 500   | 0     | 1.37   |
| Phison    | Driven OEM SSDs        | 8      | 67      | 487   | 0     | 1.34   |
| Crucial   | BX/MX1/2/3/500, M5/... | 10     | 34      | 540   | 1     | 1.32   |
| MyDigi... | Unknown                | 2      | 2       | 475   | 0     | 1.30   |
| Intel     | 520 Series SSDs        | 6      | 13      | 1503  | 548   | 1.29   |
| CWDISK    | Unknown                | 1      | 1       | 455   | 0     | 1.25   |
| SanDisk   | SanDisk based SSDs     | 19     | 46      | 481   | 3     | 1.24   |
| AEGO      | Unknown                | 1      | 1       | 445   | 0     | 1.22   |
| TCSUNBOW  | Unknown                | 1      | 3       | 429   | 0     | 1.18   |
| Micron    | BX/MX1/2/3/500, M5/... | 5      | 12      | 404   | 1     | 1.10   |
| SanDisk   | Marvell based SanDi... | 30     | 79      | 460   | 2     | 1.10   |
| Toshiba   | OCZ                    | 2      | 2       | 368   | 0     | 1.01   |
| AVEXIR    | Unknown                | 1      | 1       | 365   | 0     | 1.00   |
| Micron    | 5100 Pro / 52x0 / 5... | 2      | 3       | 364   | 0     | 1.00   |
| Toshiba   | Unknown                | 13     | 18      | 373   | 12    | 1.00   |
| OWC       | SandForce Driven SSDs  | 4      | 9       | 357   | 0     | 0.98   |
| Plextor   | M3/M5/M6/M7 Series ... | 7      | 7       | 488   | 1     | 0.96   |
| Samsung   | Unknown                | 16     | 29      | 350   | 1     | 0.96   |
| SK hynix  | Unknown                | 4      | 5       | 465   | 65    | 0.95   |
| Mushkin   | Unknown                | 3      | 3       | 334   | 0     | 0.92   |
| Smartbuy  | Phison Driven SSDs     | 1      | 1       | 327   | 0     | 0.90   |
| PNY       | Phison Driven SSDs     | 5      | 24      | 326   | 0     | 0.89   |
| SPCC      | Phison Driven OEM SSDs | 7      | 37      | 313   | 0     | 0.86   |
| Hyundai   | Unknown                | 1      | 1       | 306   | 0     | 0.84   |
| Vaseky    | Unknown                | 2      | 2       | 293   | 0     | 0.81   |
| HP        | Unknown                | 6      | 7       | 293   | 0     | 0.81   |
| Intel     | 545s Series SSDs       | 3      | 7       | 291   | 0     | 0.80   |
| Hoodisk   | Phison Driven OEM SSDs | 5      | 77      | 286   | 0     | 0.78   |
| SMART     | Unknown                | 1      | 1       | 280   | 0     | 0.77   |
| Apacer    | SDM4 Series SSD Module | 1      | 5       | 412   | 3     | 0.74   |
| Apple     | Unknown                | 2      | 2       | 268   | 0     | 0.74   |
| WDC       | Blue / Red / Green ... | 11     | 42      | 264   | 0     | 0.72   |
| SanDisk   | Unknown                | 36     | 41      | 299   | 49    | 0.72   |
| Kingston  | JMicron/Maxiotek ba... | 2      | 2       | 905   | 4     | 0.71   |
| Intel     | Unknown                | 11     | 17      | 388   | 133   | 0.65   |
| Micron    | BX/MX1/2/3/500, M5/... | 2      | 7       | 1181  | 157   | 0.64   |
| Transcend | JMicron/Maxiotek ba... | 1      | 1       | 230   | 0     | 0.63   |
| Faspeed   | Unknown                | 1      | 1       | 230   | 0     | 0.63   |
| Seagate   | Unknown                | 4      | 4       | 448   | 1     | 0.62   |
| Kingston  | SSDNow UV400/500       | 7      | 64      | 222   | 0     | 0.61   |
| Corsair   | Indilinx Barefoot b... | 1      | 1       | 221   | 0     | 0.61   |
| Kingston  | Phison Driven SSDs     | 11     | 100     | 209   | 1     | 0.57   |
| OCZ       | OCZ/Toshiba Trion SSDs | 2      | 2       | 207   | 0     | 0.57   |
| Kingston  | Unknown                | 16     | 22      | 311   | 237   | 0.56   |
| Intenso   | Phison Driven OEM SSDs | 2      | 2       | 199   | 0     | 0.55   |
| OCZ       | Indilinx Barefoot_2... | 3      | 3       | 523   | 2     | 0.54   |
| SPCC      | Unknown                | 1      | 2       | 197   | 0     | 0.54   |
| Patriot   | Phison Driven SSDs     | 2      | 8       | 195   | 0     | 0.54   |
| Apacer    | SSDs                   | 1      | 1       | 187   | 0     | 0.51   |
| Apple     | SD/SM/TS E/F/G SSDs    | 6      | 9       | 311   | 14    | 0.51   |
| AMD       | Unknown                | 1      | 1       | 183   | 0     | 0.50   |
| KingDian  | Unknown                | 1      | 1       | 177   | 0     | 0.49   |
| Crucial   | BX/MX1/2/3/500, M5/... | 3      | 6       | 291   | 6     | 0.48   |
| Transcend | Unknown                | 11     | 17      | 200   | 61    | 0.48   |
| SK hynix  | SATA SSDs              | 7      | 9       | 302   | 18    | 0.47   |
| Patriot   | Unknown                | 1      | 1       | 172   | 0     | 0.47   |
| Crucial   | Client SSDs            | 13     | 75      | 201   | 1     | 0.46   |
| Intenso   | Unknown                | 7      | 14      | 159   | 4     | 0.44   |
| Indilinx  | Unknown                | 2      | 2       | 157   | 0     | 0.43   |
| Apacer    | SDM5/5A/5A-M Series... | 3      | 5       | 794   | 34    | 0.42   |
| Zheino    | Unknown                | 4      | 5       | 153   | 0     | 0.42   |
| KingDian  | Silicon Motion base... | 4      | 6       | 151   | 169   | 0.41   |
| Dogfish   | Unknown                | 5      | 7       | 172   | 1     | 0.39   |
| Intenso   | Silicon Motion base... | 1      | 2       | 138   | 0     | 0.38   |
| ADATA     | Unknown                | 10     | 15      | 158   | 71    | 0.37   |
| KingSpec  | Unknown                | 8      | 11      | 134   | 0     | 0.37   |
| Micron    | Client SSDs            | 4      | 4       | 130   | 0     | 0.36   |
| Intel     | X25-E SSDs             | 2      | 2       | 118   | 0     | 0.33   |
| Crucial   | MX500 SSDs             | 3      | 47      | 121   | 1     | 0.32   |
| ADATA     | Silicon Motion base... | 6      | 20      | 148   | 71    | 0.30   |
| Intel     | Dell Certified Inte... | 1      | 2       | 105   | 0     | 0.29   |
| WDC       | Blue and Green SSDs    | 10     | 68      | 120   | 1     | 0.28   |
| Micron    | Unknown                | 7      | 10      | 219   | 372   | 0.28   |
| Micron    | RealSSD m4/C400/P400   | 3      | 5       | 107   | 202   | 0.27   |
| BlueRay   | Unknown                | 1      | 1       | 95    | 0     | 0.26   |
| Pioneer   | Unknown                | 2      | 2       | 94    | 0     | 0.26   |
| Transcend | Silicon Motion base... | 28     | 83      | 92    | 0     | 0.25   |
| EMTEC     | Unknown                | 3      | 3       | 89    | 0     | 0.25   |
| China     | Unknown                | 32     | 37      | 100   | 3     | 0.24   |
| Goodram   | Unknown                | 2      | 2       | 87    | 0     | 0.24   |
| Apacer    | Unknown                | 6      | 8       | 197   | 1     | 0.24   |
| PNY       | Unknown                | 5      | 8       | 86    | 0     | 0.24   |
| UDinfo    | Unknown                | 1      | 3       | 82    | 0     | 0.23   |
| Goodram   | Phison Driven SSDs     | 1      | 1       | 76    | 0     | 0.21   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 1      | 4       | 75    | 0     | 0.21   |
| Lite-On   | Unknown                | 17     | 18      | 83    | 57    | 0.20   |
| Kston     | Unknown                | 3      | 8       | 100   | 1     | 0.19   |
| ZTC       | Unknown                | 2      | 3       | 399   | 9     | 0.19   |
| KingFast  | Unknown                | 4      | 14      | 109   | 70    | 0.19   |
| Drevo     | Silicon Motion base... | 2      | 3       | 66    | 0     | 0.18   |
| Plextor   | M3/M5/M6 Series SSDs   | 1      | 2       | 64    | 0     | 0.18   |
| Verbatim  | Unknown                | 2      | 2       | 58    | 0     | 0.16   |
| Intel     | 510 Series SSDs        | 1      | 2       | 57    | 0     | 0.16   |
| BIWIN     | Unknown                | 3      | 9       | 57    | 0     | 0.16   |
| Transcend | SandForce Driven SSDs  | 1      | 2       | 170   | 3     | 0.16   |
| Dogfish   | Silicon Motion base... | 3      | 11      | 55    | 0     | 0.15   |
| Intel     | S4510/S4610/S4500/S... | 5      | 16      | 54    | 0     | 0.15   |
| Team      | Unknown                | 2      | 2       | 52    | 0     | 0.15   |
| KingSpec  | JMicron/Maxiotek ba... | 2      | 5       | 52    | 0     | 0.14   |
| Lenovo    | Unknown                | 1      | 1       | 50    | 0     | 0.14   |
| MidasF... | Unknown                | 1      | 1       | 32    | 0     | 0.09   |
| OCZ       | Indilinx Barefoot b... | 1      | 2       | 298   | 56    | 0.09   |
| Gigabyte  | Phison Driven SSDs     | 2      | 5       | 30    | 0     | 0.08   |
| Kingston  | Silicon Motion base... | 1      | 1       | 28    | 0     | 0.08   |
| FORESEE   | Unknown                | 4      | 19      | 26    | 0     | 0.07   |
| Apacer    | AS340 SSDs             | 1      | 1       | 25    | 0     | 0.07   |
| ORICO     | Unknown                | 1      | 1       | 19    | 0     | 0.05   |
| MicroD... | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| Protectli | Unknown                | 5      | 11      | 17    | 0     | 0.05   |
| Lite-On   | Silicon Motion base... | 1      | 1       | 13    | 0     | 0.04   |
| NTC       | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| ATP       | Unknown                | 5      | 8       | 12    | 0     | 0.03   |
| Hikvision | Unknown                | 2      | 2       | 11    | 0     | 0.03   |
| Leven     | Unknown                | 1      | 1       | 9     | 0     | 0.03   |
| MEMXPRO   | Unknown                | 1      | 2       | 4     | 0     | 0.01   |
| Corsair   | Unknown                | 1      | 1       | 678   | 149   | 0.01   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 1      | 1       | 3     | 0     | 0.01   |
| Lexar     | Unknown                | 4      | 4       | 3     | 2     | 0.01   |
| OWC       | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| SMI       | Unknown                | 2      | 2       | 282   | 1209  | 0.01   |
| KingFast  | Silicon Motion base... | 1      | 1       | 1     | 0     | 0.00   |
| Wintec    | Unknown                | 1      | 1       | 1431  | 1017  | 0.00   |
| Netac     | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| VisionTek | Unknown                | 1      | 2       | 777   | 1016  | 0.00   |
| BAITITON  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| minisf... | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| QUMO      | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison | Unknown                | 1      | 1       | 105   | 1067  | 0.00   |
| KLLISRE   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Intel     | 540 Series SSDs        | 2      | 2       | 20    | 520   | 0.00   |
| INDMEM    | Unknown                | 1      | 1       | 0     | 0     | 0.00   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| HPE         | 5      | 9       | 1244  | 1     | 3.33   |
| Dell        | 1      | 2       | 1173  | 0     | 3.22   |
| AMD         | 2      | 3       | 955   | 0     | 2.62   |
| OCZ         | 18     | 30      | 1122  | 51    | 2.32   |
| SuperMicro  | 3      | 3       | 824   | 0     | 2.26   |
| Corsair     | 11     | 14      | 1175  | 156   | 2.09   |
| Intel       | 71     | 148     | 960   | 92    | 1.84   |
| Mushkin     | 5      | 5       | 639   | 0     | 1.75   |
| Samsung     | 121    | 434     | 661   | 3     | 1.74   |
| Seagate     | 5      | 6       | 721   | 1     | 1.57   |
| V-GeN       | 1      | 1       | 500   | 0     | 1.37   |
| Phison      | 8      | 67      | 487   | 0     | 1.34   |
| Toshiba     | 21     | 30      | 486   | 7     | 1.32   |
| MyDigita... | 2      | 2       | 475   | 0     | 1.30   |
| Goodram     | 5      | 8       | 467   | 0     | 1.28   |
| CWDISK      | 1      | 1       | 455   | 0     | 1.25   |
| AEGO        | 1      | 1       | 445   | 0     | 1.22   |
| TCSUNBOW    | 1      | 3       | 429   | 0     | 1.18   |
| SanDisk     | 88     | 188     | 449   | 12    | 1.12   |
| Innodisk    | 4      | 4       | 394   | 0     | 1.08   |
| ADATA       | 27     | 50      | 407   | 58    | 1.02   |
| Plextor     | 11     | 12      | 447   | 1     | 1.00   |
| AVEXIR      | 1      | 1       | 365   | 0     | 1.00   |
| Kingston    | 52     | 256     | 397   | 28    | 0.90   |
| Smartbuy    | 1      | 1       | 327   | 0     | 0.90   |
| OWC         | 5      | 10      | 322   | 0     | 0.88   |
| SPCC        | 8      | 39      | 307   | 0     | 0.84   |
| Apple       | 10     | 14      | 387   | 9     | 0.84   |
| Hyundai     | 1      | 1       | 306   | 0     | 0.84   |
| Vaseky      | 2      | 2       | 293   | 0     | 0.81   |
| HP          | 6      | 7       | 293   | 0     | 0.81   |
| Hoodisk     | 5      | 77      | 286   | 0     | 0.78   |
| Crucial     | 34     | 176     | 321   | 7     | 0.78   |
| Micron      | 24     | 45      | 457   | 130   | 0.77   |
| SMART       | 1      | 1       | 280   | 0     | 0.77   |
| PNY         | 10     | 32      | 266   | 0     | 0.73   |
| SK hynix    | 11     | 14      | 360   | 35    | 0.64   |
| Team        | 3      | 3       | 234   | 0     | 0.64   |
| Faspeed     | 1      | 1       | 230   | 0     | 0.63   |
| Patriot     | 3      | 9       | 193   | 0     | 0.53   |
| WDC         | 21     | 110     | 175   | 1     | 0.45   |
| Intenso     | 10     | 18      | 161   | 3     | 0.44   |
| Indilinx    | 2      | 2       | 157   | 0     | 0.43   |
| Zheino      | 4      | 5       | 153   | 0     | 0.42   |
| KingDian    | 5      | 7       | 154   | 145   | 0.42   |
| Apacer      | 12     | 20      | 391   | 10    | 0.41   |
| Transcend   | 43     | 105     | 123   | 10    | 0.32   |
| KingSpec    | 10     | 16      | 108   | 0     | 0.30   |
| BlueRay     | 1      | 1       | 95    | 0     | 0.26   |
| Pioneer     | 2      | 2       | 94    | 0     | 0.26   |
| EMTEC       | 3      | 3       | 89    | 0     | 0.25   |
| China       | 32     | 37      | 100   | 3     | 0.24   |
| Dogfish     | 8      | 18      | 101   | 1     | 0.24   |
| UDinfo      | 1      | 3       | 82    | 0     | 0.23   |
| SATADOM     | 1      | 4       | 75    | 0     | 0.21   |
| Kston       | 3      | 8       | 100   | 1     | 0.19   |
| ZTC         | 2      | 3       | 399   | 9     | 0.19   |
| Lite-On     | 18     | 19      | 79    | 54    | 0.19   |
| Drevo       | 2      | 3       | 66    | 0     | 0.18   |
| KingFast    | 5      | 15      | 102   | 65    | 0.17   |
| Verbatim    | 2      | 2       | 58    | 0     | 0.16   |
| BIWIN       | 3      | 9       | 57    | 0     | 0.16   |
| Lenovo      | 1      | 1       | 50    | 0     | 0.14   |
| MidasForce  | 1      | 1       | 32    | 0     | 0.09   |
| Gigabyte    | 2      | 5       | 30    | 0     | 0.08   |
| FORESEE     | 4      | 19      | 26    | 0     | 0.07   |
| ORICO       | 1      | 1       | 19    | 0     | 0.05   |
| MicroDream  | 1      | 1       | 18    | 0     | 0.05   |
| Protectli   | 5      | 11      | 17    | 0     | 0.05   |
| NTC         | 1      | 1       | 12    | 0     | 0.03   |
| ATP         | 5      | 8       | 12    | 0     | 0.03   |
| Hikvision   | 2      | 2       | 11    | 0     | 0.03   |
| Leven       | 1      | 1       | 9     | 0     | 0.03   |
| MEMXPRO     | 1      | 2       | 4     | 0     | 0.01   |
| Lexar       | 4      | 4       | 3     | 2     | 0.01   |
| SMI         | 2      | 2       | 282   | 1209  | 0.01   |
| Wintec      | 1      | 1       | 1431  | 1017  | 0.00   |
| Netac       | 1      | 1       | 1     | 0     | 0.00   |
| VisionTek   | 1      | 2       | 777   | 1016  | 0.00   |
| BAITITON    | 1      | 1       | 0     | 0     | 0.00   |
| minisforum  | 1      | 1       | 0     | 0     | 0.00   |
| QUMO        | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison   | 1      | 1       | 105   | 1067  | 0.00   |
| KLLISRE     | 1      | 1       | 0     | 0     | 0.00   |
| INDMEM      | 1      | 1       | 0     | 0     | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See complete list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Intel     | SSDPEDMW400G4      | 400 GB | 2       | 1410  | 0     | 3.86   |
| Plextor   | PX-256M8PeY        | 256 GB | 1       | 1218  | 0     | 3.34   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 1       | 1195  | 0     | 3.28   |
| Samsung   | SSD 950 PRO        | 512 GB | 2       | 1098  | 0     | 3.01   |
| Kingston  | SKC1000240G        | 240 GB | 1       | 934   | 0     | 2.56   |
| Samsung   | MZVPV256HDGL-000L7 | 256 GB | 1       | 915   | 0     | 2.51   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 1       | 827   | 0     | 2.27   |
| Samsung   | SSD 950 PRO        | 256 GB | 1       | 1495  | 1     | 2.05   |
| Transcend | TS256GMTE110S      | 256 GB | 1       | 730   | 0     | 2.00   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 1       | 674   | 0     | 1.85   |
| HP        | SSD EX900          | 120 GB | 2       | 637   | 0     | 1.75   |
| Intel     | SSDPEKKW128G8      | 128 GB | 1       | 599   | 0     | 1.64   |
| Plextor   | PX-256M8PeG        | 256 GB | 1       | 598   | 0     | 1.64   |
| Samsung   | MZFLV512HCJH-000MV | 512 GB | 1       | 554   | 0     | 1.52   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 1       | 550   | 0     | 1.51   |
| HP        | SSD EX920          | 512 GB | 1       | 531   | 0     | 1.46   |
| Patriot   | Scorch M2          | 128 GB | 1       | 493   | 0     | 1.35   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 1       | 446   | 0     | 1.22   |
| Intel     | SSDPE21D280GA      | 280 GB | 1       | 432   | 0     | 1.18   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 2       | 429   | 0     | 1.18   |
| Samsung   | SSD 960 EVO        | 250 GB | 13      | 401   | 0     | 1.10   |
| Crucial   | CT500P1SSD8        | 500 GB | 2       | 381   | 0     | 1.05   |
| SPCC      | M.2 PCIE SSD       | 256 GB | 1       | 376   | 0     | 1.03   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 1       | 367   | 0     | 1.01   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 1       | 363   | 0     | 1.00   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 1       | 333   | 0     | 0.91   |
| ADATA     | SX6000NP           | 128 GB | 2       | 324   | 0     | 0.89   |
| Samsung   | SSD 970 PRO        | 512 GB | 6       | 313   | 0     | 0.86   |
| Corsair   | Force MP600        | 2 TB   | 1       | 308   | 0     | 0.85   |
| Intel     | SSDPED1D480GA      | 480 GB | 1       | 299   | 0     | 0.82   |
| Kingston  | SA1000M8240G       | 240 GB | 1       | 298   | 0     | 0.82   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 2       | 297   | 0     | 0.81   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 1       | 293   | 0     | 0.80   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 1       | 286   | 0     | 0.78   |
| Samsung   | SSD 960 EVO        | 500 GB | 5       | 283   | 0     | 0.78   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 4       | 278   | 0     | 0.76   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 1       | 277   | 0     | 0.76   |
| Samsung   | SSD 970 EVO        | 250 GB | 5       | 266   | 0     | 0.73   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 2       | 265   | 0     | 0.73   |
| Samsung   | SSD 960 PRO        | 512 GB | 1       | 262   | 0     | 0.72   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 1       | 257   | 0     | 0.71   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 1       | 239   | 0     | 0.66   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 3       | 235   | 0     | 0.65   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 3       | 226   | 0     | 0.62   |
| Phison    | Sabrent            | 1 TB   | 7       | 225   | 0     | 0.62   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 3       | 221   | 0     | 0.61   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 218   | 0     | 0.60   |
| Silico... | R5MP240G8          | 240 GB | 1       | 218   | 0     | 0.60   |
| Samsung   | PM951 NVMe         | 256 GB | 1       | 215   | 0     | 0.59   |
| PNY       | CS3030 500GB SSD   | 500 GB | 2       | 206   | 0     | 0.57   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 1       | 199   | 0     | 0.55   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 5       | 198   | 0     | 0.54   |
| ADATA     | SX8200PNP          | 1 TB   | 4       | 194   | 0     | 0.53   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 1       | 172   | 0     | 0.47   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 1       | 172   | 0     | 0.47   |
| Intel     | SSDPEKNW512G8      | 512 GB | 2       | 170   | 0     | 0.47   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 2       | 170   | 0     | 0.47   |
| Intel     | SSDPEDMW800G4      | 800 GB | 1       | 168   | 0     | 0.46   |
| Corsair   | Force MP510        | 240 GB | 3       | 162   | 0     | 0.45   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 3       | 161   | 0     | 0.44   |
| Corsair   | Force MP510        | 480 GB | 1       | 155   | 0     | 0.43   |
| Toshiba   | RC100              | 240 GB | 1       | 151   | 0     | 0.41   |
| ORICO     | V500               | 1 TB   | 1       | 149   | 0     | 0.41   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 6       | 187   | 1     | 0.40   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 2       | 147   | 0     | 0.40   |
| Samsung   | SSD 970 EVO        | 1 TB   | 7       | 146   | 0     | 0.40   |
| SK hynix  | BC501 NVMe         | 512 GB | 1       | 141   | 0     | 0.39   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 1       | 140   | 0     | 0.38   |
| ADATA     | IM2P33F8BR1-512GB  | 512 GB | 1       | 137   | 0     | 0.38   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 5       | 136   | 0     | 0.37   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 4       | 133   | 0     | 0.37   |
| Toshiba   | THNSF5256GCJ7      | 256 GB | 1       | 130   | 0     | 0.36   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 10      | 129   | 0     | 0.35   |
| ADATA     | SX8200NP           | 480 GB | 1       | 124   | 0     | 0.34   |
| Samsung   | PM961 NVMe         | 512 GB | 1       | 116   | 0     | 0.32   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 1       | 115   | 0     | 0.32   |
| Samsung   | SSD 970 EVO        | 500 GB | 11      | 111   | 0     | 0.30   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 1       | 111   | 0     | 0.30   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 1       | 109   | 0     | 0.30   |
| Intel     | SSDPEKKW512G7      | 512 GB | 2       | 173   | 1     | 0.30   |
| HP        | SSD EX920          | 256 GB | 1       | 108   | 0     | 0.30   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 6       | 105   | 0     | 0.29   |
| Corsair   | Force MP300        | 120 GB | 1       | 102   | 0     | 0.28   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 1       | 98    | 0     | 0.27   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 1       | 97    | 0     | 0.27   |
| Samsung   | MZVLW512HMJP-000H7 | 512 GB | 1       | 96    | 0     | 0.26   |
| ADATA     | SX6000LNP          | 128 GB | 1       | 96    | 0     | 0.26   |
| Silico... | NE-256             | 256 GB | 1       | 95    | 0     | 0.26   |
| Corsair   | Force MP600        | 500 GB | 1       | 91    | 0     | 0.25   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 1       | 89    | 0     | 0.24   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 2       | 89    | 0     | 0.24   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 4       | 85    | 0     | 0.23   |
| Kingston  | SA2000M81000G      | 1 TB   | 2       | 116   | 505   | 0.23   |
| Gigabyte  | GP-AG42TB          | 2 TB   | 2       | 83    | 0     | 0.23   |
| WDC       | PC SN730 NVMe      | 1 TB   | 1       | 83    | 0     | 0.23   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 1       | 81    | 0     | 0.22   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 1       | 80    | 0     | 0.22   |
| Samsung   | SSD 970 PRO        | 1 TB   | 3       | 79    | 0     | 0.22   |
| Phison    | PCIe SSD           | 500 GB | 3       | 76    | 0     | 0.21   |
| Kingston  | SA2000M8250G       | 250 GB | 6       | 73    | 0     | 0.20   |
| HP        | SSD EX950          | 512 GB | 10      | 68    | 0     | 0.19   |
| Kingston  | OM8PCP3512F-AI1    | 512 GB | 1       | 65    | 0     | 0.18   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 9       | 65    | 0     | 0.18   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 11      | 64    | 0     | 0.18   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 3       | 60    | 0     | 0.17   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 2       | 60    | 0     | 0.17   |
| SK hynix  | PC611 NVMe         | 512 GB | 1       | 56    | 0     | 0.15   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 2       | 55    | 0     | 0.15   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 1       | 53    | 0     | 0.15   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 3       | 51    | 0     | 0.14   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 12      | 49    | 0     | 0.14   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 1       | 48    | 0     | 0.13   |
| Union ... | UMIS LENSE40256... | 256 GB | 2       | 47    | 0     | 0.13   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 1       | 41    | 0     | 0.11   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 1       | 41    | 0     | 0.11   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 1       | 40    | 0     | 0.11   |
| Samsung   | PM981 NVMe         | 256 GB | 1       | 40    | 0     | 0.11   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 1       | 39    | 0     | 0.11   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 2       | 36    | 0     | 0.10   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 4       | 36    | 0     | 0.10   |
| Enmotus   | P200-1600-128      | 1.5 TB | 1       | 34    | 0     | 0.09   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 1       | 33    | 0     | 0.09   |
| Samsung   | SSD 960 EVO        | 1 TB   | 2       | 91    | 2     | 0.09   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 1       | 32    | 0     | 0.09   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 2       | 32    | 0     | 0.09   |
| Crucial   | CT2000P5SSD8       | 2 TB   | 1       | 32    | 0     | 0.09   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 1       | 30    | 0     | 0.08   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 6       | 30    | 0     | 0.08   |
| Phison    | minisforum         | 512 GB | 2       | 28    | 0     | 0.08   |
| WDC       | PC SN520 NVMe      | 256 GB | 1       | 28    | 0     | 0.08   |
| Seagate   | FireCuda 520 SS... | 500 GB | 2       | 27    | 0     | 0.08   |
| Samsung   | SSD 980 PRO        | 250 GB | 1       | 27    | 0     | 0.08   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 4       | 27    | 0     | 0.07   |
| Samsung   | MZALQ128HBHQ-000L1 | 128 GB | 5       | 26    | 0     | 0.07   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 1       | 25    | 0     | 0.07   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 1       | 25    | 0     | 0.07   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 1       | 23    | 0     | 0.07   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 2       | 23    | 0     | 0.06   |
| ATP       | NVMe M.2 2280 SSD  | 240 GB | 2       | 23    | 0     | 0.06   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 2       | 22    | 0     | 0.06   |
| Colorful  | CN600              | 512 GB | 1       | 22    | 0     | 0.06   |
| SK hynix  | PC401 NVMe         | 256 GB | 1       | 22    | 0     | 0.06   |
| ADATA     | SX8200PNP          | 512 GB | 1       | 22    | 0     | 0.06   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 1       | 22    | 0     | 0.06   |
| SK hynix  | BC511 NVMe         | 512 GB | 2       | 21    | 0     | 0.06   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 2       | 20    | 0     | 0.06   |
| Kingston  | SA2000M8500G       | 500 GB | 2       | 19    | 0     | 0.05   |
| Gigabyte  | GP-GSM2NE3128GNTD  | 128 GB | 1       | 18    | 0     | 0.05   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 1       | 18    | 0     | 0.05   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 2       | 18    | 0     | 0.05   |
| Samsung   | PM991 NVMe         | 256 GB | 2       | 15    | 0     | 0.04   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 1       | 15    | 0     | 0.04   |
| Phison    | Sabrent Rocket ... | 1 TB   | 1       | 14    | 0     | 0.04   |
| Micron    | 2200S NVMe         | 1 TB   | 2       | 13    | 0     | 0.04   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 1       | 11    | 0     | 0.03   |
| Gigabyte  | GP-GSM2NE3256GNTD  | 256 GB | 1       | 11    | 0     | 0.03   |
| Lite-On   | CA3-8D512          | 512 GB | 1       | 10    | 0     | 0.03   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 10    | 0     | 0.03   |
| SK hynix  | PC300 HFS512GD9... | 512 GB | 1       | 10    | 0     | 0.03   |
| Mushkin   | MKNSSDHL500GB-D8   | 500 GB | 2       | 8     | 0     | 0.02   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 2       | 7     | 0     | 0.02   |
| Union ... | UMIS LENSE40512... | 512 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | OM8PDP3512B-A01    | 512 GB | 5       | 6     | 0     | 0.02   |
| Silico... | Aura Pro X2        | 960 GB | 1       | 6     | 0     | 0.02   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 1       | 5     | 0     | 0.02   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 1       | 5     | 0     | 0.01   |
| Toshiba   | KBG30ZMV256G KI... | 256 GB | 1       | 5     | 0     | 0.01   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 2       | 5     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 1       | 5     | 0     | 0.01   |
| Crucial   | CT500P5SSD8        | 500 GB | 3       | 5     | 0     | 0.01   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 1       | 5     | 0     | 0.01   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 1       | 4     | 0     | 0.01   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 1       | 4     | 0     | 0.01   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 1       | 4     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 1       | 3     | 0     | 0.01   |
| SanDisk   | Ultra 3D NVMe      | 500 GB | 1       | 3     | 0     | 0.01   |
| Phison    | APS-SE20G-256      | 256 GB | 1       | 2     | 0     | 0.01   |
| T-FORCE   | TM8FP7001T         | 1 TB   | 1       | 2     | 0     | 0.01   |
| Samsung   | SSD 980            | 250 GB | 1       | 2     | 0     | 0.01   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | SSD 980 PRO        | 2 TB   | 2       | 2     | 0     | 0.01   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 2       | 2     | 0     | 0.01   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 1       | 2     | 0     | 0.01   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 1       | 1     | 0     | 0.01   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 1       | 1     | 0     | 0.00   |
| Union ... | RPFTJ128PDD2EWX    | 128 GB | 1       | 1     | 0     | 0.00   |
| Pioneer   | APS-SE10N-256      | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | SSD 980 PRO        | 500 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | PM981 NVMe         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Micron    | 2200S NVMe         | 512 GB | 1       | 1     | 0     | 0.00   |
| SK hynix  | PC611 NVMe         | 256 GB | 1       | 0     | 0     | 0.00   |
| Solid ... | CL1-3D128-Q11 N... | 128 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | KXG60PNV2T04 NV... | 2 TB   | 1       | 0     | 0     | 0.00   |
| Kingston  | OM8PDP3256B-A01    | 256 GB | 2       | 0     | 0     | 0.00   |
| SK hynix  | HFM512GDHTNG-8310A | 512 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | SX8200PNP          | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLB512HBJQ-000   | 512 GB | 1       | 0     | 0     | 0.00   |
| EMTEC     | X300               | 128 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | SX6000LNP          | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 980            | 500 GB | 1       | 0     | 0     | 0.00   |
| Silico... | 500GB-PRO-X-SS     | 500 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 980 PRO        | 1 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WDS500G1X0E-00AFY0 | 500 GB | 1       | 0     | 0     | 0.00   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| Plextor     | 2      | 2       | 908   | 0     | 2.49   |
| Transcend   | 1      | 1       | 730   | 0     | 2.00   |
| Patriot     | 1      | 1       | 493   | 0     | 1.35   |
| Intel       | 18     | 36      | 261   | 1     | 0.71   |
| HP          | 4      | 14      | 185   | 0     | 0.51   |
| Toshiba     | 15     | 18      | 180   | 0     | 0.50   |
| SPCC        | 4      | 7       | 180   | 0     | 0.49   |
| Samsung     | 58     | 165     | 171   | 1     | 0.45   |
| Corsair     | 6      | 8       | 156   | 0     | 0.43   |
| ADATA       | 8      | 12      | 150   | 0     | 0.41   |
| ORICO       | 1      | 1       | 149   | 0     | 0.41   |
| PNY         | 2      | 4       | 119   | 0     | 0.33   |
| Lenovo      | 1      | 1       | 115   | 0     | 0.32   |
| Phison      | 7      | 19      | 106   | 0     | 0.29   |
| Crucial     | 6      | 14      | 105   | 0     | 0.29   |
| WDC         | 25     | 41      | 104   | 0     | 0.29   |
| Kingston    | 10     | 22      | 95    | 46    | 0.25   |
| Silicon ... | 4      | 4       | 80    | 0     | 0.22   |
| Seagate     | 2      | 3       | 55    | 0     | 0.15   |
| Gigabyte    | 5      | 7       | 42    | 0     | 0.12   |
| Enmotus     | 1      | 1       | 34    | 0     | 0.09   |
| Union Me... | 3      | 4       | 25    | 0     | 0.07   |
| SK hynix    | 14     | 18      | 23    | 0     | 0.07   |
| ATP         | 1      | 2       | 23    | 0     | 0.06   |
| Colorful    | 1      | 1       | 22    | 0     | 0.06   |
| KIOXIA      | 1      | 1       | 22    | 0     | 0.06   |
| Lite-On     | 1      | 1       | 10    | 0     | 0.03   |
| Mushkin     | 1      | 2       | 8     | 0     | 0.02   |
| Micron      | 3      | 5       | 7     | 0     | 0.02   |
| SanDisk     | 1      | 1       | 3     | 0     | 0.01   |
| T-FORCE     | 1      | 1       | 2     | 0     | 0.01   |
| Pioneer     | 1      | 1       | 1     | 0     | 0.00   |
| Solid St... | 1      | 1       | 0     | 0     | 0.00   |
| EMTEC       | 1      | 1       | 0     | 0     | 0.00   |

