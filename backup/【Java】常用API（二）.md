

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括Math类，System类，Runtime类，BigDecimal类，Date类，SimpleDateFormat类，以及Calendar类

2.笔记对应视频119~122节

# 更新记录

无

# Math类

工具类，存储对数据进行操作的一些静态方法

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080753180.png)

Apis6.java

```Java
package com.zbhgis.apis;

public class Apis6 {
    public static void main(String[] args) {
        System.out.println(Math.abs(-12));
        System.out.println(Math.abs(-453));
        System.out.println(Math.ceil(1.000001));
        System.out.println(Math.ceil(1.0));
        System.out.println(Math.floor(3.9999999));
        System.out.println(Math.floor(4.0));
        System.out.println(Math.max(2, 4.1));
        System.out.println(Math.min(-3, 3.10));
        System.out.println(Math.pow(2,3));
        System.out.println(Math.pow(4,0.5));
        System.out.println(Math.random());
    }
}
```

打印结果

```Plain
12
453
2.0
1.0
3.0
4.0
4.1
-3.0
8.0
2.0
0.9595126408716304
```

# System类

代表程序所在的系统，也是一个工具类

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080753704.png)

Apis7.java

```Java
package com.zbhgis.apis;

public class Apis7 {
    public static void main(String[] args) {
        // System.exit(0);
        long time = System.currentTimeMillis();
        System.out.println(time);
        for (int i = 0; i < 10000; i++) {
            System.out.print("");
        }
        System.out.println(System.currentTimeMillis()-time);
    }
}
```

 打印结果

```Plain
1767277605560
2
```

# Runtime类

代表程序所在的运行环境，是一个单例类

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080753057.png)

Apis8.java

```Java
package com.zbhgis.apis;

import java.io.IOException;

public class Apis8 {
    // 添加异常检测
    public static void main(String[] args) throws IOException, InterruptedException {
        Runtime r = Runtime.getRuntime();
        // r.exit(0);
        System.out.println(r.availableProcessors());
        System.out.println(r.totalMemory()/1024/1024+"MB");
        System.out.println(r.freeMemory());

        Process p = r.exec("D:\\Program Files\\Tencent\\QQNT\\QQ.exe");
        Thread.sleep(5000);
        p.destroy();
    }
}
```

打印结果

```Plain
20
508MB
528482304
```

# BigDecimal类

用于解决浮点型运算时，结果失真的问题

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080753176.png)

Apis9.java

```Java
package com.zbhgis.apis;

import java.math.BigDecimal;
import java.math.RoundingMode;

public class Apis9 {
    public static void main(String[] args) {
        double a = 0.1;
        double b = 0.3;
        BigDecimal a1 = BigDecimal.valueOf(a);
        BigDecimal b1 = BigDecimal.valueOf(b);
        BigDecimal c1 = a1.add(b1);
        BigDecimal c2 = a1.subtract(b1);
        BigDecimal c3 = a1.multiply(b1);
        BigDecimal c4 = a1.divide(b1, 2, RoundingMode.HALF_UP);
        System.out.println(c1);
        System.out.println(c2);
        System.out.println(c3);
        System.out.println(c4);
        System.out.println(c1.doubleValue());
    }
}
```

打印结果

```Plain
0.4
-0.2
0.03
0.33
```

# Date类

代表日期和时间

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080752562.png)

Apis10.java

```Java
package com.zbhgis.apis;

import java.util.Date;

public class Apis10 {
    public static void main(String[] args) {
        Date d = new Date();
        System.out.println(d);

        long time = d.getTime();
        System.out.println(time);

        time += 2 * 1000;
        Date d2 = new Date(time);
        System.out.println(d2);

        Date d3 = new Date();
        d3.setTime(time);
        System.out.println(d3);
    }
}
```

打印结果

```Plain
Fri Jan 02 10:30:14 CST 2026
1767321014896
Fri Jan 02 10:30:16 CST 2026
Fri Jan 02 10:30:16 CST 2026
```

# SimpleDateFormat类

对时间格式进行转换

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080752688.png)

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080752669.png)

时间格式的常见符号

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080755604.png)

Apis11.java

```Java
package com.zbhgis.apis;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Apis11 {
    public static void main(String[] args) throws ParseException {
        Date d = new Date();
        System.out.println(d);

        long time = d.getTime();
        System.out.println(time);

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss EEE a");
        String rs = sdf.format(d);
        String rs2 = sdf.format(time);

        System.out.println(rs);
        System.out.println(rs2);
        System.out.println();

        String dateStr = "2022-12-12 12:12:11";
        SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Date d2 = sdf2.parse(dateStr);
        System.out.println(d2);
    }
}
```

打印结果

```Plain
Fri Jan 02 11:07:23 CST 2026
1767323243516
2026年01月02日 11:07:23 周五 上午
2026年01月02日 11:07:23 周五 上午

Mon Dec 12 12:12:11 CST 2022
```

# Calendar类

代表的是系统此刻时间对应的日历，通过它可以单独获取和修改时间中的年月日时分秒

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080753135.png)

Apis12.java

```Java
package com.zbhgis.apis;

import java.util.Calendar;
import java.util.Date;

public class Apis12 {
    public static void main(String[] args) {
        Calendar now = Calendar.getInstance();
        System.out.println(now);

        int year = now.get(Calendar.YEAR);
        int week = now.get(Calendar.WEEK_OF_YEAR);
        System.out.println(year);
        System.out.println(week);

        Date d = now.getTime();
        System.out.println(d);

        long time = now.getTimeInMillis();
        System.out.println(time);

        now.set(Calendar.MONTH, 9);
        now.set(Calendar.HOUR, 1);
        System.out.println(now);

        now.add(Calendar.HOUR, -20);
        System.out.println(now.getTime());
    }
}
```

打印结果

```OpenGL
java.util.GregorianCalendar[time=1767324440273,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2026,MONTH=0,WEEK_OF_YEAR=1,WEEK_OF_MONTH=1,DAY_OF_MONTH=2,DAY_OF_YEAR=2,DAY_OF_WEEK=6,DAY_OF_WEEK_IN_MONTH=1,AM_PM=0,HOUR=11,HOUR_OF_DAY=11,MINUTE=27,SECOND=20,MILLISECOND=273,ZONE_OFFSET=28800000,DST_OFFSET=0]
2026
1
Fri Jan 02 11:27:20 CST 2026
1767324440273
java.util.GregorianCalendar[time=?,areFieldsSet=false,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2026,MONTH=9,WEEK_OF_YEAR=1,WEEK_OF_MONTH=1,DAY_OF_MONTH=2,DAY_OF_YEAR=2,DAY_OF_WEEK=6,DAY_OF_WEEK_IN_MONTH=1,AM_PM=0,HOUR=1,HOUR_OF_DAY=11,MINUTE=27,SECOND=20,MILLISECOND=273,ZONE_OFFSET=28800000,DST_OFFSET=0]
Thu Oct 01 05:27:20 CST 2026
```

# LocalDate、LocalTime、LocalDateTime类（新增）

jdk8之后的新的时间类

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080753516.png)

Apis13.java

```Java
package com.zbhgis.apis;

import java.time.LocalDateTime;

public class Apis13 {
    public static void main(String[] args) {
        LocalDateTime ldt = LocalDateTime.now();
        System.out.println(ldt);

        int year = ldt.getYear();
        int month = ldt.getMonthValue();
        int day = ldt.getDayOfMonth();
        int doy = ldt.getDayOfYear();
        int dow = ldt.getDayOfWeek().getValue();
        System.out.println(year);
        System.out.println(day);
        System.out.println(dow);

        LocalDateTime ldt2 = ldt.withYear(2099);
        LocalDateTime ldt3 = ldt.withMonth(12);
        System.out.println(ldt2);
        System.out.println(ldt3);

        LocalDateTime ldt4 = ldt.plusYears(2);
        LocalDateTime ldt5 = ldt.plusMonths(2);
        LocalDateTime ldt6 = ldt.minusYears(4);
        LocalDateTime ldt7 = ldt.minusDays(400);
        LocalDateTime ldt8 = LocalDateTime.of(2099, 12,11,2,3,5);
        LocalDateTime ldt9 = LocalDateTime.of(2099, 11,11,4,3,2);;

        System.out.println(ldt4);
        System.out.println(ldt5);
        System.out.println(ldt6);
        System.out.println(ldt7);
        System.out.println(ldt8);
        System.out.println(ldt9);

        System.out.println(ldt8.equals(ldt9));
        System.out.println(ldt9.isAfter(ldt8));
        System.out.println(ldt9.isBefore(ldt8));

        LocalDateTime ldt10 = LocalDateTime.of(ldt.toLocalDate(), ldt.toLocalTime());
        System.out.println(ldt10);
    }
}
```

打印结果

```Plain
2026-01-02T21:20:21.760051200
2026
2
5
2099-01-02T21:20:21.760051200
2026-12-02T21:20:21.760051200
2028-01-02T21:20:21.760051200
2026-03-02T21:20:21.760051200
2022-01-02T21:20:21.760051200
2024-11-28T21:20:21.760051200
2099-12-11T02:03:05
2099-11-11T04:03:02
false
false
true
2026-01-02T21:20:21.760051200
```

# ZoneId、ZoneDateTime类（新增）

时区与时区时间

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080752416.png)

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080754630.png)

Apis14.java

```Java
package com.zbhgis.apis;

import java.time.Clock;
import java.time.ZoneId;
import java.time.ZonedDateTime;

public class Apis14 {
    public static void main(String[] args) {
        ZoneId zoneId = ZoneId.systemDefault();
        System.out.println(zoneId.getId());
        System.out.println(zoneId);
        System.out.println(ZoneId.getAvailableZoneIds());

        ZoneId zoneId1 = ZoneId.of("America/New_York");
        ZonedDateTime now = ZonedDateTime.now(zoneId1);
        System.out.println(now);

        ZonedDateTime now1 = ZonedDateTime.now(Clock.systemUTC());
        System.out.println(now1);

        ZonedDateTime now2 = ZonedDateTime.now();
        System.out.println(now2);
    }
}
```

打印结果

```Plain
Asia/Shanghai
Asia/Shanghai
[Asia/Aden, America/Cuiaba, Etc/GMT+9, Etc/GMT+8, Africa/Nairobi, America/Marigot, Asia/Aqtau, Pacific/Kwajalein, America/El_Salvador, Asia/Pontianak, Africa/Cairo, Pacific/Pago_Pago, Africa/Mbabane, Asia/Kuching, Pacific/Honolulu, Pacific/Rarotonga, America/Guatemala, Australia/Hobart, Europe/London, America/Belize, America/Panama, Asia/Chungking, America/Managua, America/Indiana/Petersburg, Asia/Yerevan, Europe/Brussels, GMT, Europe/Warsaw, America/Chicago, Asia/Kashgar, Chile/Continental, Pacific/Yap, CET, Etc/GMT-1, Etc/GMT-0, Europe/Jersey, America/Tegucigalpa, Etc/GMT-5, Europe/Istanbul, America/Eirunepe, Etc/GMT-4, America/Miquelon, Etc/GMT-3, Europe/Luxembourg, Etc/GMT-2, Etc/GMT-9, America/Argentina/Catamarca, Etc/GMT-8, Etc/GMT-7, Etc/GMT-6, Europe/Zaporozhye, Canada/Yukon, Canada/Atlantic, Atlantic/St_Helena, Australia/Tasmania, Libya, Europe/Guernsey, America/Grand_Turk, Asia/Samarkand, America/Argentina/Cordoba, Asia/Phnom_Penh, Africa/Kigali, Asia/Almaty, US/Alaska, Asia/Dubai, Europe/Isle_of_Man, America/Araguaina, Cuba, Asia/Novosibirsk, America/Argentina/Salta, Etc/GMT+3, Africa/Tunis, Etc/GMT+2, Etc/GMT+1, Pacific/Fakaofo, Africa/Tripoli, Etc/GMT+0, Israel, Africa/Banjul, Etc/GMT+7, Indian/Comoro, Etc/GMT+6, Etc/GMT+5, Etc/GMT+4, Pacific/Port_Moresby, US/Arizona, Antarctica/Syowa, Indian/Reunion, Pacific/Palau, Europe/Kaliningrad, America/Montevideo, Africa/Windhoek, Asia/Karachi, Africa/Mogadishu, Australia/Perth, Brazil/East, Etc/GMT, Asia/Chita, Pacific/Easter, Antarctica/Davis, Antarctica/McMurdo, Asia/Macao, America/Manaus, Africa/Freetown, Europe/Bucharest, Asia/Tomsk, America/Argentina/Mendoza, Asia/Macau, Europe/Malta, Mexico/BajaSur, Pacific/Tahiti, Africa/Asmera, Europe/Busingen, America/Argentina/Rio_Gallegos, Africa/Malabo, Europe/Skopje, America/Catamarca, America/Godthab, Europe/Sarajevo, Australia/ACT, GB-Eire, Africa/Lagos, America/Cordoba, Europe/Rome, Asia/Dacca, Indian/Mauritius, Pacific/Samoa, America/Regina, America/Fort_Wayne, America/Dawson_Creek, Africa/Algiers, Europe/Mariehamn, America/St_Johns, America/St_Thomas, Europe/Zurich, America/Anguilla, Asia/Dili, America/Denver, Africa/Bamako, Europe/Saratov, GB, Mexico/General, Pacific/Wallis, Europe/Gibraltar, Africa/Conakry, Africa/Lubumbashi, Asia/Istanbul, America/Havana, NZ-CHAT, Asia/Choibalsan, America/Porto_Acre, Asia/Omsk, Europe/Vaduz, US/Michigan, Asia/Dhaka, America/Barbados, Europe/Tiraspol, Atlantic/Cape_Verde, Asia/Yekaterinburg, America/Louisville, Pacific/Johnston, Pacific/Chatham, Europe/Ljubljana, America/Sao_Paulo, Asia/Jayapura, America/Curacao, Asia/Dushanbe, America/Guyana, America/Guayaquil, America/Martinique, Portugal, Europe/Berlin, Europe/Moscow, Europe/Chisinau, America/Puerto_Rico, America/Rankin_Inlet, Pacific/Ponape, Europe/Stockholm, Europe/Budapest, America/Argentina/Jujuy, Australia/Eucla, Asia/Shanghai, Universal, Europe/Zagreb, America/Port_of_Spain, Europe/Helsinki, Asia/Beirut, Asia/Tel_Aviv, Pacific/Bougainville, US/Central, Africa/Sao_Tome, Indian/Chagos, America/Cayenne, Asia/Yakutsk, Pacific/Galapagos, Australia/North, Europe/Paris, Africa/Ndjamena, Pacific/Fiji, America/Rainy_River, Indian/Maldives, Australia/Yancowinna, SystemV/AST4, Asia/Oral, America/Yellowknife, Pacific/Enderbury, America/Juneau, Australia/Victoria, America/Indiana/Vevay, Asia/Tashkent, Asia/Jakarta, Africa/Ceuta, Asia/Barnaul, America/Recife, America/Buenos_Aires, America/Noronha, America/Swift_Current, Australia/Adelaide, America/Metlakatla, Africa/Djibouti, America/Paramaribo, Asia/Qostanay, Europe/Simferopol, Europe/Sofia, Africa/Nouakchott, Europe/Prague, America/Indiana/Vincennes, Antarctica/Mawson, America/Kralendijk, Antarctica/Troll, Europe/Samara, Indian/Christmas, America/Antigua, Pacific/Gambier, America/Indianapolis, America/Inuvik, America/Iqaluit, Pacific/Funafuti, UTC, Antarctica/Macquarie, Canada/Pacific, America/Moncton, Africa/Gaborone, Pacific/Chuuk, Asia/Pyongyang, America/St_Vincent, Asia/Gaza, Etc/Universal, PST8PDT, Atlantic/Faeroe, Asia/Qyzylorda, Canada/Newfoundland, America/Kentucky/Louisville, America/Yakutat, Asia/Ho_Chi_Minh, Antarctica/Casey, Europe/Copenhagen, Africa/Asmara, Atlantic/Azores, Europe/Vienna, ROK, Pacific/Pitcairn, America/Mazatlan, Australia/Queensland, Pacific/Nauru, Europe/Tirane, Asia/Kolkata, SystemV/MST7, Australia/Canberra, MET, Australia/Broken_Hill, Europe/Riga, America/Dominica, Africa/Abidjan, America/Mendoza, America/Santarem, Kwajalein, America/Asuncion, Asia/Ulan_Bator, NZ, America/Boise, Australia/Currie, EST5EDT, Pacific/Guam, Pacific/Wake, Atlantic/Bermuda, America/Costa_Rica, America/Dawson, Asia/Chongqing, Eire, Europe/Amsterdam, America/Indiana/Knox, America/North_Dakota/Beulah, Africa/Accra, Atlantic/Faroe, Mexico/BajaNorte, America/Maceio, Etc/UCT, Pacific/Apia, GMT0, America/Atka, Pacific/Niue, Australia/Lord_Howe, Europe/Dublin, Pacific/Truk, MST7MDT, America/Monterrey, America/Nassau, America/Jamaica, Asia/Bishkek, America/Atikokan, Atlantic/Stanley, Australia/NSW, US/Hawaii, SystemV/CST6, Indian/Mahe, Asia/Aqtobe, America/Sitka, Asia/Vladivostok, Africa/Libreville, Africa/Maputo, Zulu, America/Kentucky/Monticello, Africa/El_Aaiun, Africa/Ouagadougou, America/Coral_Harbour, Pacific/Marquesas, Brazil/West, America/Aruba, America/North_Dakota/Center, America/Cayman, Asia/Ulaanbaatar, Asia/Baghdad, Europe/San_Marino, America/Indiana/Tell_City, America/Tijuana, Pacific/Saipan, SystemV/YST9, Africa/Douala, America/Chihuahua, America/Ojinaga, Asia/Hovd, America/Anchorage, Chile/EasterIsland, America/Halifax, Antarctica/Rothera, America/Indiana/Indianapolis, US/Mountain, Asia/Damascus, America/Argentina/San_Luis, America/Santiago, Asia/Baku, America/Argentina/Ushuaia, Atlantic/Reykjavik, Africa/Brazzaville, Africa/Porto-Novo, America/La_Paz, Antarctica/DumontDUrville, Asia/Taipei, Antarctica/South_Pole, Asia/Manila, Asia/Bangkok, Africa/Dar_es_Salaam, Poland, Atlantic/Madeira, Antarctica/Palmer, America/Thunder_Bay, Africa/Addis_Ababa, Asia/Yangon, Europe/Uzhgorod, Brazil/DeNoronha, Asia/Ashkhabad, Etc/Zulu, America/Indiana/Marengo, America/Creston, America/Punta_Arenas, America/Mexico_City, Antarctica/Vostok, Asia/Jerusalem, Europe/Andorra, US/Samoa, PRC, Asia/Vientiane, Pacific/Kiritimati, America/Matamoros, America/Blanc-Sablon, Asia/Riyadh, Iceland, Pacific/Pohnpei, Asia/Ujung_Pandang, Atlantic/South_Georgia, Europe/Lisbon, Asia/Harbin, Europe/Oslo, Asia/Novokuznetsk, CST6CDT, Atlantic/Canary, America/Knox_IN, Asia/Kuwait, SystemV/HST10, Pacific/Efate, Africa/Lome, America/Bogota, America/Menominee, America/Adak, Pacific/Norfolk, Europe/Kirov, America/Resolute, Pacific/Kanton, Pacific/Tarawa, Africa/Kampala, Asia/Krasnoyarsk, Greenwich, SystemV/EST5, America/Edmonton, Europe/Podgorica, Australia/South, Canada/Central, Africa/Bujumbura, America/Santo_Domingo, US/Eastern, Europe/Minsk, Pacific/Auckland, Africa/Casablanca, America/Glace_Bay, Canada/Eastern, Asia/Qatar, Europe/Kiev, Singapore, Asia/Magadan, SystemV/PST8, America/Port-au-Prince, Europe/Belfast, America/St_Barthelemy, Asia/Ashgabat, Africa/Luanda, America/Nipigon, Atlantic/Jan_Mayen, Brazil/Acre, Asia/Muscat, Asia/Bahrain, Europe/Vilnius, America/Fortaleza, Etc/GMT0, US/East-Indiana, America/Hermosillo, America/Cancun, Africa/Maseru, Pacific/Kosrae, Africa/Kinshasa, Asia/Kathmandu, Asia/Seoul, Australia/Sydney, America/Lima, Australia/LHI, America/St_Lucia, Europe/Madrid, America/Bahia_Banderas, America/Montserrat, Asia/Brunei, America/Santa_Isabel, Canada/Mountain, America/Cambridge_Bay, Asia/Colombo, Australia/West, Indian/Antananarivo, Australia/Brisbane, Indian/Mayotte, US/Indiana-Starke, Asia/Urumqi, US/Aleutian, Europe/Volgograd, America/Lower_Princes, America/Vancouver, Africa/Blantyre, America/Rio_Branco, America/Danmarkshavn, America/Detroit, America/Thule, Africa/Lusaka, Asia/Hong_Kong, Iran, America/Argentina/La_Rioja, Africa/Dakar, SystemV/CST6CDT, America/Tortola, America/Porto_Velho, Asia/Sakhalin, Etc/GMT+10, America/Scoresbysund, Asia/Kamchatka, Asia/Thimbu, Africa/Harare, Etc/GMT+12, Etc/GMT+11, Navajo, America/Nome, Europe/Tallinn, Turkey, Africa/Khartoum, Africa/Johannesburg, Africa/Bangui, Europe/Belgrade, Jamaica, Africa/Bissau, Asia/Tehran, WET, Europe/Astrakhan, Africa/Juba, America/Campo_Grande, America/Belem, Etc/Greenwich, Asia/Saigon, America/Ensenada, Pacific/Midway, America/Jujuy, Africa/Timbuktu, America/Bahia, America/Goose_Bay, America/Virgin, America/Pangnirtung, Asia/Katmandu, America/Phoenix, Africa/Niamey, America/Whitehorse, Pacific/Noumea, Asia/Tbilisi, America/Montreal, Asia/Makassar, America/Argentina/San_Juan, Hongkong, UCT, Asia/Nicosia, America/Indiana/Winamac, SystemV/MST7MDT, America/Argentina/ComodRivadavia, America/Boa_Vista, America/Grenada, Asia/Atyrau, Australia/Darwin, Asia/Khandyga, Asia/Kuala_Lumpur, Asia/Famagusta, Asia/Thimphu, Asia/Rangoon, Europe/Bratislava, Asia/Calcutta, America/Argentina/Tucuman, Asia/Kabul, Indian/Cocos, Japan, Pacific/Tongatapu, America/New_York, Etc/GMT-12, Etc/GMT-11, America/Nuuk, Etc/GMT-10, SystemV/YST9YDT, Europe/Ulyanovsk, Etc/GMT-14, Etc/GMT-13, W-SU, America/Merida, EET, America/Rosario, Canada/Saskatchewan, America/St_Kitts, Arctic/Longyearbyen, America/Fort_Nelson, America/Caracas, America/Guadeloupe, Asia/Hebron, Indian/Kerguelen, SystemV/PST8PDT, Africa/Monrovia, Asia/Ust-Nera, Egypt, Asia/Srednekolymsk, America/North_Dakota/New_Salem, Asia/Anadyr, Australia/Melbourne, Asia/Irkutsk, America/Shiprock, America/Winnipeg, Europe/Vatican, Asia/Amman, Etc/UTC, SystemV/AST4ADT, Asia/Tokyo, America/Toronto, Asia/Singapore, Australia/Lindeman, America/Los_Angeles, SystemV/EST5EDT, Pacific/Majuro, America/Argentina/Buenos_Aires, Europe/Nicosia, Pacific/Guadalcanal, Europe/Athens, US/Pacific, Europe/Monaco]
2026-01-02T08:36:23.260641700-05:00[America/New_York]
2026-01-02T13:36:23.263704200Z
2026-01-02T21:36:23.263704200+08:00[Asia/Shanghai]
```

# Instant类（新增）

获取时间线上的某个时刻或时间戳

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080752677.png)

Apis15.java

```Java
package com.zbhgis.apis;

import java.time.Instant;

public class Apis15 {
    public static void main(String[] args) {
        Instant now = Instant.now();

        long second = now.getEpochSecond();
        System.out.println(second);

        int nano = now.getNano();
        System.out.println(nano);

        System.out.println(now);

        Instant instant = now.plusNanos(111);
        System.out.println(now);
        
        // 可用于性能分析
        Instant now1 = Instant.now();
        for (int i = 0; i < 10000; i++) {
            System.out.print("");
        }
        Instant now2 = Instant.now();
        System.out.println(now1);
        System.out.println(now2);
    }
}
```

打印结果

```Plain
1767423410
663485300
2026-01-03T06:56:50.663485300Z
2026-01-03T06:56:50.663485300Z
2026-01-03T06:56:50.666901800Z
2026-01-03T06:56:50.667920Z
```

# DateTimeFormatter类（新增）

时间格式化

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080754092.png)

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080752942.png)

Apis16.java

```Java
package com.zbhgis.apis;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class Apis16 {
    public static void main(String[] args) {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH:mm:ss");

        LocalDateTime now = LocalDateTime.now();
        System.out.println(now);

        String rs = formatter.format(now);
        System.out.println(rs);

        String rs2 = now.format(formatter);
        System.out.println(rs2);
    }
}
```

打印结果

```Plain
2026-01-03T15:03:28.173527500
2026年01月03日 15:03:28
2026年01月03日 15:03:28
```

# Period类（新增）

计算两个LocalDate对象相差的年数，月数，天数

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080752236.png)

Apis17.java

```Java
package com.zbhgis.apis;

import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.Period;

public class Apis17 {
    public static void main(String[] args) {
        LocalDate start = LocalDate.of(2029, 8, 10);
        LocalDate end = LocalDate.of(2029, 12, 15);

        Period period = Period.between(start, end);

        System.out.println(period.getYears());
        System.out.println(period.getMonths());
        System.out.println(period.getDays());

    }
}
```

打印结果

```Plain
0
4
5
```

# Duration类（新增）

可以用于计算两个时间对象相差的天数、小时数、分数、秒数、纳秒数；支持LocalTime、LocalDateTime、Instant等时间。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080752087.png)

Apis18.java

```Java
package com.zbhgis.apis;

import java.time.Duration;
import java.time.LocalDateTime;

public class Apis18 {
    public static void main(String[] args) {
        LocalDateTime start = LocalDateTime.of(2025, 11, 11, 10, 10, 7);
        LocalDateTime end = LocalDateTime.of(2025, 11, 12, 10, 0, 7);

        Duration duration = Duration.between(start, end);

        System.out.println(duration.toDays());
        System.out.println(duration.toHours());
        System.out.println(duration.toMinutes());
        System.out.println(duration.toSeconds());
        System.out.println(duration.toMillis());
        System.out.println(duration.toNanos());
    }

}
```

打印结果

```Plain
0
23
1430
85800
85800000
85800000000000
```

# 总结

多练多写就记住了