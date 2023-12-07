![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/0ca2d4c9-1297-4532-b361-ae4e43dd3da3)



### AWS SQS

메시지를 queue에서 빼오는 것만으로는 SQS에서 메시지가 삭제되지 않습니다. 이 메시지를 처리한 후, 처리가 완료되었다(ACK)는 것을 SQS에 다시 요청해야 queue에서 메시지가 삭제되는 것입니다. 반대로, 메시지 처리가 실패한다면, 이 메시지 처리를 재시도할 수 있도록 SQS에 취소 요청(NACK)합니다.

AWS Kinesis, Apache Kafka와 같은 다른 messaging queue는 “어디까지 처리했다”와 같은 checkpoint 방식으로 메시지의 처리를 관리하는데, 메시지 하나하나에 대해 개별적으로 ACK/NACK를 보낼 수 있다는 점이 SQS의 특징입니다.
