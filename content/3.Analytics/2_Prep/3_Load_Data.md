---
title: "拷贝模拟数据"
chapter: false
weight: 33
---

7， 登陆到ec2上，使用s3 cp命令将模拟数据上传到S3上

aws s3 cp s3://jack-lab/e2e/10000871.csv s3://jack-lab/e2e/data_source/10000871.csv
