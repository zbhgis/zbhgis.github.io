

个人主页：https://github.com/zbhgis

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括LocalDate类，LocalTime类，LocalDateTime类，ZoneId类，ZoneDateTime类，Instant类，DateTimeFormatter类，Period类，Duration类以及Arrays类

2.笔记对应视频123~125节

# 更新记录

无

# LocalDate、LocalTime、LocalDateTime类（新增）

jdk8之后的新的时间类

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131002943.png)

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

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131001681.png)

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131002419.png)

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

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131002179.png)

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

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131002987.png)

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131001726.png)

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

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131001615.png)

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

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131002495.png)

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

# Arrays类

用于操作数组

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131002088.png)

Apis19.java

```Java
package com.zbhgis.apis;

import java.lang.reflect.Array;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.function.IntToDoubleFunction;

public class Apis19 {
    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40, 50, 60};
        System.out.println(Arrays.toString(arr));

        int[] arr2 = Arrays.copyOfRange(arr, 3,4);
        System.out.println(Arrays.toString(arr2));

        int[] arr3 = Arrays.copyOf(arr, 10);
        System.out.println(Arrays.toString(arr3));

        double[] prices = {99.8, 124, 10};
        Arrays.setAll(prices, new IntToDoubleFunction() {
            @Override
            public double applyAsDouble(int value) {
                return prices[value] * 0.8;
            }
        });

        System.out.println(Arrays.toString(prices));

        Arrays.sort(prices);
        System.out.println(Arrays.toString(prices));
    }
}
```

打印结果

```Plain
[10, 20, 30, 40, 50, 60]
[40]
[10, 20, 30, 40, 50, 60, 0, 0, 0, 0]
[79.84, 99.2, 8.0]
[8.0, 79.84, 99.2]
```

数组中的对象进行排序

方法一：让该对象的类实现Comparable（比较规则)接口，然后重写compareTo方法，自己来制定比较规则。

方法二：使用下面这个sort方法，创建comparator比较器接口的匿名内部类对象，然后自己制定比较规则。

People.java

```TypeScript
package com.zbhgis.apis;

public class People implements Comparable<People>{
    private String name;
    private int age;
    private double height;

    @Override
    public int compareTo(People p) {
        return this.age - p.age;
    }

    public People() {
    }

    public People(String name, int age, double height) {
        this.name = name;
        this.age = age;
        this.height = height;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public double getHeight() {
        return height;
    }

    public void setHeight(double height) {
        this.height = height;
    }

    @Override
    public String toString() {
        return "People{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", height=" + height +
                '}';
    }
}
```

Apis20.java

```Java
package com.zbhgis.apis;

import java.util.Arrays;
import java.util.Comparator;

public class Apis20 {
    public static void main(String[] args) {
        People[] peoples = new People[4];
        peoples[0] = new People("山", 11, 139);
        peoples[1] = new People("重", 11, 141);
        peoples[2] = new People("水", 10, 140);
        peoples[3] = new People("复", 23, 200);

        Arrays.sort(peoples);
        System.out.println(Arrays.toString(peoples));

        Arrays.sort(peoples, new Comparator<People>() {
            @Override
            public int compare(People o1, People o2) {
                return Double.compare(o1.getHeight(), o2.getHeight());
            }
        });
        System.out.println(Arrays.toString(peoples));
    }
}
```

打印结果

```SQL
[People{name='水', age=10, height=140.0}, People{name='山', age=11, height=139.0}, People{name='重', age=11, height=141.0}, People{name='复', age=23, height=200.0}]
[People{name='山', age=11, height=139.0}, People{name='水', age=10, height=140.0}, People{name='重', age=11, height=141.0}, People{name='复', age=23, height=200.0}]
```

# 总结

多练多写就记住了