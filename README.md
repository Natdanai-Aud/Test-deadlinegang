# SonarQube

<img width="1382" height="858" alt="Screenshot 2026-10-11 161119" src="https://github.com/user-attachments/assets/838f6984-5fa2-404f-a0a5-4b5efd602297" />


## ตารางสรุปผล (Overall Code)

| ตัวชี้วัด | ค่า | Rating |
|---|---|---|
| Bugs | 0 | A |
| Vulnerabilities | 0 | A |
| Security Hotspots Reviewed | — (ไม่มี hotspot) | A |
| Code Smells | 0 | A |
| Debt | 0 | A |
| Coverage | 51.0% (จาก 39 lines to cover) | — |
| Unit Tests | — | — |
| Duplications | 0.0% (0 blocks) | — |
  
**สิ่งที่ต้องแก้: Coverage ต่ำ (51.0%)**
```bash
src/bus-stops/bus-stops.service.ts
src/bus-stops/bus-stops.controller.ts
src/app.controller.ts
```

<img width="1315" height="417" alt="image" src="https://github.com/user-attachments/assets/9cf000f9-07bf-4d7b-b655-bc016c4456de" />

# K6

## 1. Configuration สำหรับ Load Test (ทดสอบรองรับโหลดปกติ/สูงสุดตามสเปก)

```bash
  █ THRESHOLDS

    checks
    ✗ 'rate>0.99' rate=98.28%

    http_req_duration
    ✗ 'p(95)<500' p(95)=745.8ms

      {endpoint:attractions}
      ✓ 'p(95)<500' p(95)=66.78ms

      {endpoint:parks-districts}
      ✗ 'p(95)<500' p(95)=1.04s

      {endpoint:parks-search}
      ✓ 'p(95)<500' p(95)=22.63ms

    http_req_failed
    ✓ 'rate<0.01' rate=0.00%


  █ TOTAL RESULTS

    checks_total.......: 19012  57.488805/s
    checks_succeeded...: 98.28% 18685 out of 19012
    checks_failed......: 1.71%  327 out of 19012

    ✓ B1 status is 200
    ✓ B1 response time < 500ms
    ✓ B1 body has success:true
    ✓ B1 body has data.total
    ✓ B2 status is 200
    ✓ B2 response time < 500ms
    ✓ B2 body has success:true
    ✓ B2 body data is array
    ✓ B3 status is 200
    ✗ B3 response time < 500ms
      ↳  76% — ✓ 1059 / ✗ 327
    ✓ B3 body has success:true
    ✓ B3 body data is array

    HTTP
    http_req_duration................: avg=84.37ms  min=2.05ms  med=13.07ms max=1.54s    p(90)=98.09ms  p(95)=745.8ms
      { endpoint:attractions }.......: avg=33.03ms  min=10.17ms med=28.87ms max=102.61ms p(90)=58.44ms  p(95)=66.78ms
      { endpoint:parks-districts }...: avg=239.19ms min=2.05ms  med=8.71ms  max=1.54s    p(90)=874.54ms p(95)=1.04s
      { endpoint:parks-search }......: avg=8.55ms   min=3.37ms  med=5.44ms  max=47.85ms  p(90)=17.98ms  p(95)=22.63ms
      { expected_response:true }.....: avg=84.37ms  min=2.05ms  med=13.07ms max=1.54s    p(90)=98.09ms  p(95)=745.8ms
    http_req_failed..................: 0.00%  0 out of 4753
    http_reqs........................: 4753   14.372201/s

    EXECUTION
    iteration_duration...............: avg=1.08s    min=1s      med=1.01s   max=2.54s    p(90)=1.09s    p(95)=1.74s
    iterations.......................: 4753   14.372201/s
    vus..............................: 1      min=1         max=20
    vus_max..........................: 20     min=20        max=20

    NETWORK
    data_received....................: 236 MB 714 kB/s
    data_sent........................: 445 kB 1.3 kB/s



time="2026-10-11T12:43:58Z" level=error msg="thresholds on metrics 'checks, http_req_duration, http_req_duration{endpoint:parks-districts}' have been crossed"
```

## 2. Configuration สำหรับ Stress Test (หาจุดแตกหัก / Maximum Capacity)

```bash
  █ THRESHOLDS

    checks
    ✗ 'rate>0.99' rate=97.56%

    http_req_duration
    ✗ 'p(95)<500' p(95)=848.25ms

      {endpoint:attractions}
      ✗ 'p(95)<500' p(95)=1.14s

      {endpoint:parks-districts}
      ✓ 'p(95)<500' p(95)=9.11ms

      {endpoint:parks-search}
      ✓ 'p(95)<500' p(95)=35.85ms

    http_req_failed
    ✓ 'rate<0.01' rate=0.01%


  █ TOTAL RESULTS

    checks_total.......: 116520 276.936927/s
    checks_succeeded...: 97.56% 113685 out of 116520
    checks_failed......: 2.43%  2835 out of 116520

    ✓ B1 status is 200
    ✓ B1 response time < 500ms
    ✓ B1 body has success:true
    ✓ B1 body has data.total
    ✗ B2 status is 200
      ↳  99% — ✓ 7764 / ✗ 2
    ✗ B2 response time < 500ms
      ↳  63% — ✓ 4946 / ✗ 2820
    ✗ B2 body has success:true
      ↳  99% — ✓ 7764 / ✗ 2
    ✗ B2 body data is array
      ↳  99% — ✓ 7764 / ✗ 2
    ✗ B3 status is 200
      ↳  99% — ✓ 10669 / ✗ 3
    ✓ B3 response time < 500ms
    ✗ B3 body has success:true
      ↳  99% — ✓ 10669 / ✗ 3
    ✗ B3 body data is array
      ↳  99% — ✓ 10669 / ✗ 3

    HTTP
    http_req_duration................: avg=108.16ms min=0s     med=5.92ms   max=1.7s    p(90)=435.69ms p(95)=848.25ms
      { endpoint:attractions }.......: avg=384.82ms min=0s     med=141.29ms max=1.7s    p(90)=1.02s    p(95)=1.14s
      { endpoint:parks-districts }...: avg=3.73ms   min=0s     med=2.89ms   max=26.16ms p(90)=6.28ms   p(95)=9.11ms
      { endpoint:parks-search }......: avg=11.45ms  min=3.03ms med=6.47ms   max=72.1ms  p(90)=25.83ms  p(95)=35.85ms
      { expected_response:true }.....: avg=108.18ms min=1.16ms med=5.92ms   max=1.7s    p(90)=435.84ms p(95)=848.27ms
    http_req_failed..................: 0.01%  5 out of 29130
    http_reqs........................: 29130  69.234232/s

    EXECUTION
    iteration_duration...............: avg=1.11s    min=1s     med=1s       max=31s     p(90)=1.43s    p(95)=1.85s
    iterations.......................: 29130  69.234232/s
    vus..............................: 5      min=1          max=200
    vus_max..........................: 200    min=200        max=200

    NETWORK
    data_received....................: 1.2 GB 2.7 MB/s
    data_sent........................: 2.7 MB 6.5 kB/s



time="2026-10-11T12:45:38Z" level=error msg="thresholds on metrics 'checks, http_req_duration, http_req_duration{endpoint:attractions}' have been crossed"
```
