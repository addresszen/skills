# South Korea MOIS Address

A South Korean road name address (도로명주소) as published by the Ministry of the Interior and Safety (MOIS).

Every address is indexed twice, once in Hangul and once in Revised Romanization. `line_1` and `line_2` follow the language of the matched document; the API returns the underlying MOIS fields under their original Hangul names.

Korean-named fields are empty strings when the source record does not carry a value.

**Schema name:** `MoisAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `mois` | Dataset the address originates from. |  |
| `country` | yes | `South Korea` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `KOR` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `KR` | 2 letter country code (ISO 3166-1) |  |
| `language` | yes | `ko` | Language represented by 2 letter ISO Code (639-1) |  |
| `address` | yes | string | Jibeon (land lot) number: `지번본번_번지` and `지번부번_호` joined by a hyphen. |  |
| `line_1` | yes | string | First address line. |  |
| `line_2` | yes | string | Second address line. |  |
| `city` | yes | string | Preferred city name. |  |
| `province` | yes | string | Preferred province name. |  |
| `법정읍면동명` | yes | string | Legal town name. |  |
| `법정동코드` | yes | string | Legal district code. |  |
| `법정리명` | yes | string | Legal name. |  |
| `비고1` | yes | string | Note 1. |  |
| `비고2` | yes | string | Note 2. |  |
| `변동전도로명주소` | yes | string | Changed street name address. |  |
| `변경이력정보` | yes | string | Change history information. |  |
| `변경이력사유` | yes | string | Change history reason. |  |
| `변경전_도로명주소` | yes | string | Previous road name address. |  |
| `변경사유` | yes | string | Change reason. |  |
| `변경사유코드` | yes | string | Change reason code. |  |
| `층일련번호` | yes | string | Floor serial number. |  |
| `층명칭` | yes | string | Floor name. |  |
| `대표지번여부` | yes | string | Is representative address. |  |
| `대표여부` | yes | string | Is representative. |  |
| `다량배달처명` | yes | string | Bulk delivery location name. |  |
| `동일련번호` | yes | string | Building serial number. |  |
| `동명칭` | yes | string | Building name. |  |
| `도로명` | yes | string | Road name. |  |
| `도로명_로마자` | yes | string | Romanised road name. |  |
| `도로명번호` | yes | string | Road name number. |  |
| `도로명코드` | yes | string | Road name code. |  |
| `도로명코드_고시일자` | yes | string | Road name code creation date. |  |
| `도로명코드_말소일자` | yes | string | Road name code deletion date. |  |
| `읍면동구분` | yes | string | Town classification. |  |
| `읍면동일련번호` | yes | string | Town serial number. |  |
| `읍면동코드` | yes | string | Town code. |  |
| `읍면동명` | yes | string | Town name. |  |
| `읍면동명_로마자` | yes | string | Romanised town name. |  |
| `건축물대장_건물명` | yes | string | Building name in building register. |  |
| `건물본번` | yes | string | Building number. |  |
| `건물부번` | yes | string | Building sub-number. |  |
| `건물관리번호` | yes | string | Building management number. |  |
| `기초구역번호` | yes | string | Basic area number. |  |
| `공동주택여부` | yes | string | Is apartment. |  |
| `고시일자` | yes | string | Creation date. |  |
| `관리번호` | yes | string | Management number. |  |
| `행정동코드` | yes | string | Administrative district code. |  |
| `행정동명` | yes | string | Administrative district name. |  |
| `호일련번호` | yes | string | Unit serial number. |  |
| `호명칭` | yes | string | Unit name. |  |
| `호접미사일련번호` | yes | string | Unit suffix serial number. |  |
| `호접미사명칭` | yes | string | Unit suffix name. |  |
| `이동사유코드` | yes | string | Movement reason code. |  |
| `일련번호` | yes | string | Serial number. |  |
| `지번일련번호` | yes | string | Address serial number. |  |
| `지번본번_번지` | yes | string | Jibeon (land lot) main number. |  |
| `지번부번_호` | yes | string | Jibeon (land lot) sub-number. |  |
| `지하구분` | yes | string | Is basement. |  |
| `지하여부` | yes | string | Level (ground level, underground, aerial). |  |
| `산여부` | yes | string | Is mountain. |  |
| `상위도로명` | yes | string | Upper road name. |  |
| `상위도로명번호` | yes | string | Upper road name number. |  |
| `상세건물명` | yes | string | Detailed building name. |  |
| `상세주소_부여여부` | yes | string | Whether detailed address assigned. |  |
| `상세주소여부` | yes | string | Whether detailed address exists. |  |
| `사용여부` | yes | string | In use. |  |
| `시도명` | yes | string | City name. |  |
| `시도명_로마자` | yes | string | Romanised city name. |  |
| `시군구_건물명` | yes | string | District (sigungu) building name, as recorded in the address DB (주소DB). |  |
| `시군구코드` | yes | string | District code. |  |
| `시군구명` | yes | string | District name. |  |
| `시군구명_로마자` | yes | string | Romanised district name. |  |
| `시군구용_건물명` | yes | string | District (sigungu) building name, as recorded in the building and PO box DBs (건물DB, 사서함주소DB). |  |
| `우편일련번호` | yes | string | Postal sequence number. |  |
| `우편번호` | yes | string | Postal code. |  |
| `우편번호_일련번호` | yes | string | Postal code serial number. |  |
| `영문_법정리명` | yes | string | English legal name. |  |
| `영문읍면동명` | yes | string | English town name. |  |
| `영문_법정읍면동명` | yes | string | English legal town name. |  |
| `영문도로명` | yes | string | English road name. |  |
| `영문시도명` | yes | string | English city name. |  |
| `영문시군구명` | yes | string | English district name. |  |

## Example

```json
{
  "id": "mois_hM9Ur94A6Wxd8rFfQWHjKQ",
  "dataset": "mois",
  "country": "South Korea",
  "country_iso": "KOR",
  "country_iso_2": "KR",
  "language": "ko",
  "address": "108-21",
  "line_1": "종로구 청운동 자하문로 108-21",
  "line_2": "청운빌딩 100동 1호",
  "city": "서울특별시",
  "province": "서울특별시",
  "법정읍면동명": "청운동",
  "법정동코드": "1111010100",
  "법정리명": "",
  "비고1": "",
  "비고2": "",
  "변동전도로명주소": "",
  "변경이력정보": "",
  "변경이력사유": "",
  "변경전_도로명주소": "",
  "변경사유": "",
  "변경사유코드": "",
  "층일련번호": "",
  "층명칭": "",
  "대표지번여부": "",
  "대표여부": "",
  "다량배달처명": "",
  "동일련번호": "",
  "동명칭": "",
  "도로명": "자하문로",
  "도로명_로마자": "",
  "도로명번호": "3100012",
  "도로명코드": "111103100012",
  "도로명코드_고시일자": "20100702",
  "도로명코드_말소일자": "",
  "읍면동구분": "1",
  "읍면동일련번호": "01",
  "읍면동코드": "101",
  "읍면동명": "청운동",
  "읍면동명_로마자": "",
  "건축물대장_건물명": "",
  "건물본번": "100",
  "건물부번": "1",
  "건물관리번호": "1111010100101080021031434",
  "기초구역번호": "03047",
  "공동주택여부": "0",
  "고시일자": "",
  "관리번호": "",
  "행정동코드": "1111051500",
  "행정동명": "청운효자동",
  "호일련번호": "",
  "호명칭": "",
  "호접미사일련번호": "",
  "호접미사명칭": "",
  "이동사유코드": "",
  "일련번호": "",
  "지번일련번호": "",
  "지번본번_번지": "108",
  "지번부번_호": "21",
  "지하구분": "",
  "지하여부": "0",
  "산여부": "0",
  "상위도로명": "",
  "상위도로명번호": "",
  "상세건물명": "",
  "상세주소_부여여부": "",
  "상세주소여부": "0",
  "사용여부": "0",
  "시도명": "서울특별시",
  "시도명_로마자": "",
  "시군구_건물명": "",
  "시군구코드": "11110",
  "시군구명": "종로구",
  "시군구명_로마자": "",
  "시군구용_건물명": "청운빌딩",
  "우편일련번호": "",
  "우편번호": "03047",
  "우편번호_일련번호": "",
  "영문_법정리명": "",
  "영문읍면동명": "Cheongun-dong",
  "영문_법정읍면동명": "",
  "영문도로명": "Jahamun-ro",
  "영문시도명": "Seoul",
  "영문시군구명": "Jongno-gu"
}
```
