FROM ubuntu:latest

# JMeter Version 및 다운로드 URL을 수정해야 할 수 있습니다.
ENV JMETER_VERSION 5.4.3
ENV JMETER_HOME /opt/apache-jmeter-${JMETER_VERSION}
ENV PATH $JMETER_HOME/bin:$PATH

# 기본 패키지 설치
RUN apt-get update && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/*

# JMeter 다운로드 및 설치
RUN curl -Ls https://downloads.apache.org/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz | tar -xz -C /opt \
    && rm -rf ${JMETER_HOME}/docs ${JMETER_HOME}/printable_docs

# 필요한 포트 열기
EXPOSE 60000 1099 50000

# 테스트 계획 파일이 위치한 디렉토리를 컨테이너 내부로 복사
COPY testplan/ ${JMETER_HOME}/bin/testplan/

# JMeter Master 실행 스크립트
CMD ["jmeter", "-n", "-t", "/opt/apache-jmeter-${JMETER_VERSION}/bin/testplan/your_testplan.jmx", "-R", "slave1_ip,slave2_ip"]
