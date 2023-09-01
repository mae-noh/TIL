https://support.google.com/analytics/answer/7029846?hl=en#items&zippy=%2Cevent%2Citems

일일 내보내기 옵션이 활성화된 경우 각 데이터세트 내에서 이름이 지정된 테이블이 events_YYYYMMDD매일 생성   

스트리밍 내보내기 옵션이 활성화되면 이름이 지정된 테이블이  events_intraday_YYYYMMDD 생성   
이 테이블은 하루 종일 이벤트가 기록되면서 지속적으로 채워짐   
이 테이블은 매일 작업이 events_YYYYMMDD완료되면 삭제됨   

   
```
{
  O"event_date": "20230828",
  O"event_timestamp": 1693215363466006 //이벤트타임스탬프(마이크로초), 
  O"event_name": "screen_view" //이벤트명,
  O"event_params": //이벤트와관련된매개변수 [
    {
      "key": "ga_session_id",
      "value": {
        "string_value": null,
        "int_value": 1693215306,
        "float_value": null,
        "double_value": null
      }
    },
    {
      "key": "firebase_event_origin",
      "value": {
        "string_value": "auto",
        "int_value": null,
        "float_value": null,
        "double_value": null
      }
    },
    {
      "key": "firebase_previous_class",
      "value": {
        "string_value": "MainActivity",
        "int_value": null,
        "float_value": null,
        "double_value": null
      }
    },
    {
      "key": "firebase_previous_id",
      "value": {
        "string_value": null,
        "int_value": -5625624659212615000,
        "float_value": null,
        "double_value": null
      }
    },
    {
      "key": "engagement_time_msec",
      "value": {
        "string_value": null,
        "int_value": 1509,
        "float_value": null,
        "double_value": null
      }
    },
    {
      "key": "firebase_screen_class",
      "value": {
        "string_value": "TextbookActivity",
        "int_value": null,
        "float_value": null,
        "double_value": null
      }
    },
    {
      "key": "engaged_session_event",
      "value": {
        "string_value": null,
        "int_value": 1,
        "float_value": null,
        "double_value": null
      }
    },
    {
      "key": "ga_session_number",
      "value": {
        "string_value": null,
        "int_value": 16,
        "float_value": null,
        "double_value": null
      }
    },
    {
      "key": "firebase_screen_id",
      "value": {
        "string_value": null,
        "int_value": -5625624659212615000,
        "float_value": null,
        "double_value": null
      }
    }
  ],
  O"event_previous_timestamp": 1693215361195006 //이전이벤트타임스탬프(마이크로초),
  "event_value_in_usd": null,
  "event_bundle_sequence_id": 57 //*이벤트번들시퀀스ID,
  "event_server_timestamp_offset": 866657 //*이벤트서버타임스탬프오프셋,
  O"user_id": null //사용자 ID,
  O"user_pseudo_id": "5d75b47fb0566d258b7aa9da0683d9f8"//의사식별자,
  O"privacy_info": //사용자프라이버시관련정보 {
    "analytics_storage": "Yes",
    "ads_storage": "Yes",
    "uses_transient_token": "No"
  },
  O"user_properties": //사용자속성정보리스트[
    {
      "key": "ga_session_id",
      "value": {
        "string_value": null,
        "int_value": 1693215306,
        "float_value": null,
        "double_value": null,
        "set_timestamp_micros": 1693215306618000
      }
    },
    {
      "key": "first_open_time",
      "value": {
        "string_value": null,
        "int_value": 1692234000000,
        "float_value": null,
        "double_value": null,
        "set_timestamp_micros": 1692231286450000
      }
    },
    {
      "key": "ga_session_number",
      "value": {
        "string_value": null,
        "int_value": 16,
        "float_value": null,
        "double_value": null,
        "set_timestamp_micros": 1693215306618000
      }
    }
  ],
  O"user_first_touch_timestamp": 1692231286450000 //사용자첫터치타임스탬프(마이크로초),
  "user_ltv": null //사용자수명가치??,
  O"device": //이벤트발생기기정보{
    "category": "mobile",
    "mobile_brand_name": "Xiaomi",
    "mobile_model_name": "M2010J19SI",
    "mobile_marketing_name": "Redmi 9 Power",
    "mobile_os_hardware_model": "M2010J19SI",
    "operating_system": "Android",
    "operating_system_version": "Android 10",
    "vendor_id": null,
    "advertising_id": "19f5f282-8f4b-4a9d-ac98-2b272935e944",
    "language": "en-in",
    "is_limited_ad_tracking": "No",
    "time_zone_offset_seconds": 32400,
    "browser": null,
    "browser_version": null,
    "web_info": null
  },
  O"geo": //지리정보{
    "continent": "Asia",
    "country": "South Korea",
    "region": "Seoul",
    "city": "Seoul",
    "sub_continent": "Eastern Asia",
    "metro": "(not set)"
  },
  O"app_info": //앱정보{
    "id": "com.matchnow.wematchnow.dev",
    "version": "0.8.0_Dev",
    "install_store": null,
    "firebase_app_id": "1:815144645664:android:3a2210efcedd812921b845",
    "install_source": "manual_install"
  },
  O"traffic_source": //트래픽소스정보{
    "name": "(direct)",
    "medium": "(none)",
    "source": "(direct)"
  },
  O"stream_id": "5976585638" //이벤트스트림ID,
  O"platform": "ANDROID" //플랫폼정보,
  "event_dimensions": null //이벤트차원??,
  "ecommerce": null //전자상거래정보,
  "items": //아이템정보리스트[
    
  ],
  "collected_traffic_source": null //수집된트래픽소스정보,
  O"is_active_user": true//*활성사용자여부
}
```
