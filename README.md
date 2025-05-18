# 2024_top-issue-summary_WW



Type C connector對地短路事件
Case 1 

　

Artemis Jira-538

Situation

　UART Bridges missed in BmcUSBCountCheck of FFT during PVT build.

FR is 0.46% in MP stage

Task

　Solving UART bridge missing Issue since PVT stage

Action

Check “select pin”, found that it was short to GND without USB plug in.
Cut connection to find the shorting point.
Seem’s the “short” is on the Type C connector.
Sink current into this pin can fix the short.
Re-mount also can fix it. -> looked like mounting issue.
Do X-ray and board slice to check, but can’t find the shorting path.
Analyze manufacture build info, the issue only occurred on “Lotus”.
Conduct a full inspection of the "Lotus" connector before the PCBA build. The defects were found in the material before the SMT process.
RMA the defected connector. And ask for improvement  plan.
Result 

The issue was caused by a defective connector. The vendor helped fix it and then allowed it to be returned for production.

 

PDB Log 誤報事件
Case 2

　

Artemis Jira-183

Situation

After sled cycle, that have chance will record "Record time delay 300ms, FRU: 1 , enable HPDB_HS1_BUSBAR_EN" in bmc sel

Task

Investigate the root cause of issue log

Action

Replicate the issue overnight, can be reproduce easily.
Measure on the issue net, but scope can’t capture it when issue occurred.
The issue FR is positive relation to the BMC pulling frequency. ->Should be related to I2C bus.
Check I2C signal, found that when issue occurred, the “SDA” seems to be “Change to CLOCK”.
Check i2c path, found that the “SDA” net short to “SCL” of others I2C BUS.
Result 

The issue cause by the defected 4C+ connector. And it’s single case.

“附圖展示當初找到short的位置”

一張含有 螢幕擷取畫面, 圖表, 文字 的圖片

AI 產生的內容可能不正確。

 

BUSBAR事件
Case 3

　

Artemis Jira-640

Situation

[MP] System intermittently encountered unexpected reboot or HPDB power fault during L10 testing

Task

Find the root cause of the unexpected reboot

Action

The issue seemed random in the early stages and did not follow a specific PCBA, L10, or rack.
No conclusion was reached after extensive swap testing.
The factory site reviewed security camera footage and found that the issue always occurred when an operator inserted or removed another L10 in the same rack.
Suspected a power pin mating issue between the L10 and the rack BUSBAR.
On-site signal measurements revealed voltage jitter on the "sense pin" when inserting the bottom L10 while measuring on the top L10.
Result 

Since the Artemis L10 is heavier than other projects, and there were only three L10 units in one rack, the vibration during insertion or removal of the L10 has a greater impact than in other projects. Therefore, it is necessary to lower the sensitivity of the BUSBAR monitor sense pin. (Increase the filter capacitance)

“推最底層L10進入時，上層L10抓到的signal drop”

