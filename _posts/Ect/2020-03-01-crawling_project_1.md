---
title: "WEB, Crawling, 취업정보 크롤링하기"
date: 2020-03-01 16:00:28 -0400
categories: PROJECT
tags : [WEB, PROJECT]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## 개요
- 노트북을 켜면 _매일 확인하는 것들을 자동화_ 하려고한다
- python언어를 배울필요 없이 _java를 통해 클롤링_ 할예정이다
  - java가 조금 느리다고 하지만 괜찮다
  - 많은 양을 확인할것이 아니다
  - 매일 밤 aws에서 crontab으로 실행할 예정이므로 느려도 상관없다
- _도메인 주소/robots.txt_ 를 검색하여 __크롤링이 허용되는 범위에서만__ 크롤링을 할것이다
- __jsoup과 Selenium__ 을 사용해서 크롤링할 수있는데 정적인페이지-jsoup, 동적인페이지-selenum을 이용할것이다

- [Selenium 참고 사이트](https://heodolf.tistory.com/103?category=887835)

---

> Selenium은 되고, Jsoup은 안되는 이유
```
Jsoup은 HTTP Request를 사용하여 서버에 데이터를 요청하여 랜더링된 화면을 크롤링한다
SSR은 화면은 모든 부분을 서버에서 랜더링하지만
CSR은 최소한만 서버에서 랜더링하고 나머지를 브라우저에서 랜딩하기 때문에
CSR은 Jsoup이 아닌 현재 브라우저에 출력된 페이지의 소스를 파싱하는 Selenium을 이용해서 크롤링해야한다
```

>동적 웹페이지가 아니라면 Jsoup을 이용하는 것이 좋다.

```
Jsoup은 HTTP Request를 통해 웹서버에 직접 요청하기 때문에 빠른 응답을 받을 수 있다.
하지만, Selenium은 브라우저가 랜더링 된 후 페이지를 파싱하기 때문에 수집 속도가 느리다.
```

## 코드

```java
package crawler;

import java.io.IOException;
import java.util.Iterator;
import org.jsoup.*;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

public class Crawler2 {
	public static void main(String[] args) {

		String url = "https://www.jobplanet.co.kr/job_postings/search?utf8=%E2%9C%93&jp_min_overall=2.0&recruitment_type_ids%5B%5D=1&recruitment_type_ids%5B%5D=4&city_ids%5B%5D=1&city_ids%5B%5D=2&occupation_level2_ids%5B%5D=11604&order_by=score";
		Document doc = null;

		try {

			doc = Jsoup.connect(url).get();
			System.out.println(doc);
		} catch (IOException e) {
			e.printStackTrace();

		}

		Elements elements = doc.select("div .job_content");

		System.out.println("============================================================");
		Iterator<Element> dataList = elements.select("div.result_unit_info").iterator();
		int num = 1;
		while (dataList.hasNext()) {
			Element data = dataList.next();
			String title = data.select("div.result_unit_info .posting_name").text();

			String d_day = data.select("div.result_unit_info .d_day").text();	// D-3, 채용시 마감, 상시채용, 오늘마감
			String crop_name = data.select("div.result_unit_info .company_name a").text();
			String rate = data.select("div.result_unit_info .jp_data_set .rate").text();
			String pay = data.select("div.result_unit_info .jp_data_set .salary").text();
			String recommend = data.select("div.result_unit_info .jp_data_set .recommend").text();
			String ect = data.select("div.result_unit_info .result_labels").text();

			System.out.println();

			num++;
		}

		System.out.println("============================================================");

	}
}

```

### pom.xml

```xml
<!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-chrome-driver -->
<dependency>
  <groupId>org.seleniumhq.selenium</groupId>
  <artifactId>selenium-chrome-driver</artifactId>
  <version>3.141.59</version>
</dependency>
<dependency>
  <groupId>io.github.bonigarcia</groupId>
  <artifactId>webdrivermanager</artifactId>
  <version>3.8.1</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java -->
<dependency>
  <groupId>org.seleniumhq.selenium</groupId>
  <artifactId>selenium-java</artifactId>
  <version>3.141.59</version>
</dependency>

<!-- log -->
<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-simple</artifactId>
  <version>1.7.21</version>
</dependency>
```

---
## Reference
- <https://heodolf.tistory.com/104>
- <https://heodolf.tistory.com/103?category=887835>
- [maven eclipse연동](https://nowonbun.tistory.com/535)
