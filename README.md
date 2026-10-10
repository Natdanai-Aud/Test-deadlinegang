# SonarQube

<img width="1599" height="899" alt="image" src="https://github.com/user-attachments/assets/1f44c33a-08b0-4ca0-a756-d0a84b366ff4" />

# K6

## 1. Configuration สำหรับ Load Test (ทดสอบรองรับโหลดปกติ/สูงสุดตามสเปก)

```bash
  █ THRESHOLDS

    http_req_duration
    ✓ 'p(95)<500' p(95)=266.39ms

    http_req_failed
    ✓ 'rate<0.01' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......: 2690   24.301726/s
    checks_succeeded...: 99.96% 2689 out of 2690
    checks_failed......: 0.03%  1 out of 2690

    ✓ status is 200
    ✗ response time < 500ms
      ↳  99% — ✓ 1344 / ✗ 1

    HTTP
    http_req_duration..............: avg=134.81ms min=4.52ms med=153.57ms max=513.36ms p(90)=265.39ms p(95)=266.39ms
      { expected_response:true }...: avg=134.81ms min=4.52ms med=153.57ms max=513.36ms p(90)=265.39ms p(95)=266.39ms
    http_req_failed................: 0.00%  0 out of 2690
    http_reqs......................: 2690   24.301726/s

    EXECUTION
    iteration_duration.............: avg=1.27s    min=1.26s  med=1.27s    max=2.55s    p(90)=1.27s    p(95)=1.27s
    iterations.....................: 1345   12.150863/s
    vus............................: 1      min=1         max=20
    vus_max........................: 20     min=20        max=20

    NETWORK
    data_received..................: 5.1 MB 46 kB/s
    data_sent......................: 192 kB 1.7 kB/s




running (1m50.7s), 00/20 VUs, 1345 complete and 0 interrupted iterations
default ✓ [ 100% ] 00/20 VUs  1m50s
```

## 2. Configuration สำหรับ Stress Test (หาจุดแตกหัก / Maximum Capacity)

```bash
  █ TOTAL RESULTS

    checks_total.......: 16904  120.116052/s
    checks_succeeded...: 99.95% 16897 out of 16904
    checks_failed......: 0.04%  7 out of 16904

    ✓ status is 200
    ✗ response time < 500ms
      ↳  99% — ✓ 8445 / ✗ 7

    HTTP
    http_req_duration..............: avg=134.63ms min=4.31ms med=231.86ms max=1.49s p(90)=264.95ms p(95)=266.44ms
      { expected_response:true }...: avg=134.63ms min=4.31ms med=231.86ms max=1.49s p(90)=264.95ms p(95)=266.44ms
    http_req_failed................: 0.00%  0 out of 16904
    http_reqs......................: 16904  120.116052/s

    EXECUTION
    iteration_duration.............: avg=1.28s    min=1.25s  med=1.26s    max=2.83s p(90)=1.27s    p(95)=1.27s
    iterations.....................: 8452   60.058026/s
    vus............................: 5      min=1          max=199
    vus_max........................: 200    min=200        max=200

    NETWORK
    data_received..................: 33 MB  231 kB/s
    data_sent......................: 1.5 MB 10 kB/s




running (2m20.7s), 000/200 VUs, 8452 complete and 0 interrupted iterations
default ✓ [ 100% ] 000/200 VUs  2m20s
```
