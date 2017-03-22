長庚大學 大數據分析方法 作業三
================

網站資料爬取
------------

``` r
#這是R Code Chunk
##第一次使用要先安裝
##install.packages("rvest")

library(rvest)
```

    ## Warning: package 'rvest' was built under R version 3.3.3

    ## Loading required package: xml2

    ## Warning: package 'xml2' was built under R version 3.3.3

``` r
data=NULL
for(n in 1:5){
    ##目前NBA版最新頁數之index值為4606 (最新一頁不足20筆，所以我從再前一頁開始)
    i=4606-n
    pttNBA<-paste("https://www.ptt.cc/bbs/NBA/index",i,".html",sep="")
    pttContent<-read_html(pttNBA ,encoding="UTF-8")

    title <- pttContent %>% html_nodes(".title") %>% html_text()
    push <- pttContent %>% html_nodes(".nrec")  %>% html_text()
    aut <- pttContent %>% html_nodes(".author") %>% html_text()
    
    ##一頁共20筆資料，一共爬5頁分別裝在5個資料表，所以20*5=100筆
    if(n==1){
        data1=data.frame(Title=title,PushNum=push,Author=aut)
    }else if(n==2){
        data2=data.frame(Title=title,PushNum=push,Author=aut)
    }else if(n==3){
        data3=data.frame(Title=title,PushNum=push,Author=aut)
    }else if(n==4){
        data4=data.frame(Title=title,PushNum=push,Author=aut)
    }else {
        data5=data.frame(Title=title,PushNum=push,Author=aut)
    }
}

##5合1
data = rbind(data1, data2, data3, data4, data5)
##直接試印100則
print(data)
```

    ##                                                                                   Title
    ## 1                     \n\t\t\t\n\t\t\t\t[討論] Klay Thompson 現役最強3D\n\t\t\t\n\t\t\t
    ## 2            \n\t\t\t\n\t\t\t\t[新聞] 上場時間將大幅縮水 甜瓜：我能理解\n\t\t\t\n\t\t\t
    ## 3        \n\t\t\t\n\t\t\t\t[新聞] 「俠客」銅像揭幕儀式 Kobe將出席共襄盛\n\t\t\t\n\t\t\t
    ## 4                       \n\t\t\t\n\t\t\t\t(本文已被刪除) [ZachLavine08]\n\t\t\t\n\t\t\t
    ## 5                 \n\t\t\t\n\t\t\t\tRe: [討論] Klay Thompson 現役最強3D\n\t\t\t\n\t\t\t
    ## 6        \n\t\t\t\n\t\t\t\t[新聞] 鬼之切入成絕響？ 吉諾比利：籃球已經不\n\t\t\t\n\t\t\t
    ## 7         \n\t\t\t\n\t\t\t\t[新聞] 堅決反對輪休　湯普森父：打82場並不難\n\t\t\t\n\t\t\t
    ## 8                 \n\t\t\t\n\t\t\t\t[討論] 現役球員誰的三重威脅做的最好\n\t\t\t\n\t\t\t
    ## 9           \n\t\t\t\n\t\t\t\t[情報] 表弟本季在國王與鵜鶘皆拿下單場40分\n\t\t\t\n\t\t\t
    ## 10               \n\t\t\t\n\t\t\t\t[討論] 巴特勒是不是有什麼致命的缺點?\n\t\t\t\n\t\t\t
    ## 11           \n\t\t\t\n\t\t\t\t[新聞] 杜蘭特恢復練投 傳季後賽前可望復出\n\t\t\t\n\t\t\t
    ## 12                      \n\t\t\t\n\t\t\t\t[新聞] 林書豪腳傷恐先發不保？\n\t\t\t\n\t\t\t
    ## 13        \n\t\t\t\n\t\t\t\t[討論] Klay Thompson &Ray Allen三分投籃姿勢\n\t\t\t\n\t\t\t
    ## 14                         \n\t\t\t\n\t\t\t\t[討論] 製造進攻犯規的高手?\n\t\t\t\n\t\t\t
    ## 15                     \n\t\t\t\n\t\t\t\tRe: [討論] 製造進攻犯規的高手?\n\t\t\t\n\t\t\t
    ## 16           \n\t\t\t\n\t\t\t\tRe: [討論] 巴特勒是不是有什麼致命的缺點?\n\t\t\t\n\t\t\t
    ## 17         \n\t\t\t\n\t\t\t\t[討論] 美國史上最弱奧運男籃隊-2004雅典奧運\n\t\t\t\n\t\t\t
    ## 18                      \n\t\t\t\n\t\t\t\t[情報] ★今日排名(2017.03.22)★\n\t\t\t\n\t\t\t
    ## 19                     \n\t\t\t\n\t\t\t\tRe: [討論] 製造進攻犯規的高手?\n\t\t\t\n\t\t\t
    ## 20       \n\t\t\t\n\t\t\t\t[新聞] 兄弟同場較勁 咖哩哥面子、裡子都占上風\n\t\t\t\n\t\t\t
    ## 21      \n\t\t\t\n\t\t\t\t[情報] O'Neal：尼克球員的壞習慣毀掉了三角進攻\n\t\t\t\n\t\t\t
    ## 22              \n\t\t\t\n\t\t\t\t[BOX ] Warriors 112:87 Mavericks 數據\n\t\t\t\n\t\t\t
    ## 23      \n\t\t\t\n\t\t\t\tRe: [新聞] 詹姆斯抱怨：我只休2場 馬刺用了15年\n\t\t\t\n\t\t\t
    ## 24             \n\t\t\t\n\t\t\t\t[新聞] Lebron James warning Larva Ball\n\t\t\t\n\t\t\t
    ## 25           \n\t\t\t\n\t\t\t\tRe: [新聞] NBA╱小牛老闆建議 延長賽季時間\n\t\t\t\n\t\t\t
    ## 26              \n\t\t\t\n\t\t\t\t[BOX ] Spurs 100:93 Timberwolves 數據\n\t\t\t\n\t\t\t
    ## 27                    \n\t\t\t\n\t\t\t\t[BOX ] Bucks 93:90 Blazers 數據\n\t\t\t\n\t\t\t
    ## 28                           \n\t\t\t\n\t\t\t\t(本文已被刪除) [sunyeah]\n\t\t\t\n\t\t\t
    ## 29           \n\t\t\t\n\t\t\t\tRe: [新聞] NBA╱小牛老闆建議 延長賽季時間\n\t\t\t\n\t\t\t
    ## 30    \n\t\t\t\n\t\t\t\tRe: [心得] 看了單場得分50+統計，原來老大這麼強!\n\t\t\t\n\t\t\t
    ## 31                \n\t\t\t\n\t\t\t\t[BOX ] Clippers 133:109 Lakers 數據\n\t\t\t\n\t\t\t
    ## 32      \n\t\t\t\n\t\t\t\tRe: [新聞] 詹姆斯抱怨：我只休2場 馬刺用了15年\n\t\t\t\n\t\t\t
    ## 33      \n\t\t\t\n\t\t\t\tRe: [新聞] 詹姆斯抱怨：我只休2場 馬刺用了15年\n\t\t\t\n\t\t\t
    ## 34                   \n\t\t\t\n\t\t\t\t[情報] NBA Standings(2017.03.22)\n\t\t\t\n\t\t\t
    ## 35      \n\t\t\t\n\t\t\t\tRe: [新聞] 詹姆斯抱怨：我只休2場 馬刺用了15年\n\t\t\t\n\t\t\t
    ## 36      \n\t\t\t\n\t\t\t\t[花邊] LBJ警告球爸別談論他兒子 球爸表示被斷章\n\t\t\t\n\t\t\t
    ## 37                          \n\t\t\t\n\t\t\t\t(本文已被刪除) [wmigrant]\n\t\t\t\n\t\t\t
    ## 38      \n\t\t\t\n\t\t\t\t[新聞] 火氣太大了5天內3起群毆　有錢球員太任性\n\t\t\t\n\t\t\t
    ## 39      \n\t\t\t\n\t\t\t\tRe: [新聞] 詹姆斯抱怨：我只休2場 馬刺用了15年\n\t\t\t\n\t\t\t
    ## 40                    \n\t\t\t\n\t\t\t\t[情報] Hassan Whiteside右手受傷\n\t\t\t\n\t\t\t
    ## 41          \n\t\t\t\n\t\t\t\t[專欄] 球員無限制輪休 早晚會被球迷抵制LYS\n\t\t\t\n\t\t\t
    ## 42                                 \n\t\t\t\n\t\t\t\t[Live] 灰熊 @ 鵜鶘\n\t\t\t\n\t\t\t
    ## 43                                 \n\t\t\t\n\t\t\t\t[Live] 勇士 @ 小牛\n\t\t\t\n\t\t\t
    ## 44             \n\t\t\t\n\t\t\t\t[情報] Milos Teodosic談加入NBA的可能性\n\t\t\t\n\t\t\t
    ## 45               \n\t\t\t\n\t\t\t\tRe: [討論] 輪休到底對NBA是利還是弊？\n\t\t\t\n\t\t\t
    ## 46                                 \n\t\t\t\n\t\t\t\t[Live] 馬刺 @ 灰狼\n\t\t\t\n\t\t\t
    ## 47           \n\t\t\t\n\t\t\t\t[情報] Kobe-NBA唯一個對所有球隊40+的男人\n\t\t\t\n\t\t\t
    ## 48                               \n\t\t\t\n\t\t\t\t[Live] 公鹿 @ 拓荒者\n\t\t\t\n\t\t\t
    ## 49         \n\t\t\t\n\t\t\t\t[新聞] 波波維奇有個性 不甩聯盟警告繼續輪休\n\t\t\t\n\t\t\t
    ## 50          \n\t\t\t\n\t\t\t\t[新聞] 詹姆斯抱怨：我只休2場 馬刺用了15年\n\t\t\t\n\t\t\t
    ## 51               \n\t\t\t\n\t\t\t\tRe: [討論] 輪休到底對NBA是利還是弊？\n\t\t\t\n\t\t\t
    ## 52                     \n\t\t\t\n\t\t\t\t[BOX ] Pistons 96:98 Nets 數據\n\t\t\t\n\t\t\t
    ## 53                        \n\t\t\t\n\t\t\t\t[花邊] Lopez與Ibaka發生衝突\n\t\t\t\n\t\t\t
    ## 54          \n\t\t\t\n\t\t\t\t[閒聊] Udonis Haslem跟Spoelstra談球隊防守\n\t\t\t\n\t\t\t
    ## 55                                 \n\t\t\t\n\t\t\t\t[Live] 快艇 @ 湖人\n\t\t\t\n\t\t\t
    ## 56               \n\t\t\t\n\t\t\t\tRe: [討論] 輪休到底對NBA是利還是弊？\n\t\t\t\n\t\t\t
    ## 57                       \n\t\t\t\n\t\t\t\t[BOX ] Suns 97:112 Heat 數據\n\t\t\t\n\t\t\t
    ## 58                  \n\t\t\t\n\t\t\t\t[BOX ] Bulls 120:122 Raptors 數據\n\t\t\t\n\t\t\t
    ## 59               \n\t\t\t\n\t\t\t\t[BOX ] Grizzlies 82:95 Pelicans 數據\n\t\t\t\n\t\t\t
    ## 60                              \n\t\t\t\n\t\t\t\t[討論] KD何時會歸隊??\n\t\t\t\n\t\t\t
    ## 61                           \n\t\t\t\n\t\t\t\t(本文已被刪除) [MrSatan]\n\t\t\t\n\t\t\t
    ## 62        \n\t\t\t\n\t\t\t\tRe: [新聞] 被嘲笑沒關係 胡瓏貿：我有NBA夢想\n\t\t\t\n\t\t\t
    ## 63            \n\t\t\t\n\t\t\t\t[情報] Hayward拿下生涯新高38分 爵士輸球\n\t\t\t\n\t\t\t
    ## 64                 \n\t\t\t\n\t\t\t\t[新聞] 球星輪休爭議多 聯盟出手管了\n\t\t\t\n\t\t\t
    ## 65               \n\t\t\t\n\t\t\t\t[情報] NBA Power Rankings 3/20(官網)\n\t\t\t\n\t\t\t
    ## 66                   \n\t\t\t\n\t\t\t\tFw: [問卦]體育界跨領域超強三兄弟\n\t\t\t\n\t\t\t
    ## 67                    \n\t\t\t\n\t\t\t\t[情報] 金塊總教練談Harden不輪休\n\t\t\t\n\t\t\t
    ## 68       \n\t\t\t\n\t\t\t\t[花邊] 馬刺Green談為何養蛇：看他們進食很過癮\n\t\t\t\n\t\t\t
    ## 69                \n\t\t\t\n\t\t\t\t[討論] kd受傷會成就可怕勇士誕生嗎？\n\t\t\t\n\t\t\t
    ## 70    \n\t\t\t\n\t\t\t\tRe: [心得] 看了單場得分50+統計，原來老大這麼強!\n\t\t\t\n\t\t\t
    ## 71             \n\t\t\t\n\t\t\t\t[情報] Curry：要弄清如何限制弟弟的發揮\n\t\t\t\n\t\t\t
    ## 72        \n\t\t\t\n\t\t\t\tRe: [新聞] 被嘲笑沒關係 胡瓏貿：我有NBA夢想\n\t\t\t\n\t\t\t
    ## 73      \n\t\t\t\n\t\t\t\t[徵求]03/21 12點至1點高鐵總機廠前行車紀錄畫面\n\t\t\t\n\t\t\t
    ## 74                             \n\t\t\t\n\t\t\t\t(本文已被刪除) [CGary]\n\t\t\t\n\t\t\t
    ## 75         \n\t\t\t\n\t\t\t\tFw: [情報] 小威 & Stephen Curry 兵乓球之戰\n\t\t\t\n\t\t\t
    ## 76                           \n\t\t\t\n\t\t\t\t[外絮] Jerry Krause 過世\n\t\t\t\n\t\t\t
    ## 77                                 \n\t\t\t\n\t\t\t\t[Live] 公牛 @ 暴龍\n\t\t\t\n\t\t\t
    ## 78                                 \n\t\t\t\n\t\t\t\t[Live] 活塞 @ 籃網\n\t\t\t\n\t\t\t
    ## 79                                 \n\t\t\t\n\t\t\t\t[Live] 太陽 @ 熱火\n\t\t\t\n\t\t\t
    ## 80              \n\t\t\t\n\t\t\t\t[情報] 林書豪將缺席今天對活塞隊的比賽\n\t\t\t\n\t\t\t
    ## 81       \n\t\t\t\n\t\t\t\t[情報] 最愛哪個投籃？Curry：首次總決G5第四節\n\t\t\t\n\t\t\t
    ## 82  \n\t\t\t\n\t\t\t\tRe: [情報] Rondo召集08綠軍冠軍隊聚會，有人不想All\n\t\t\t\n\t\t\t
    ## 83                     \n\t\t\t\n\t\t\t\t[情報] Harden連續3場35分10助攻\n\t\t\t\n\t\t\t
    ## 84                           \n\t\t\t\n\t\t\t\t(本文已被刪除) [MrSatan]\n\t\t\t\n\t\t\t
    ## 85  \n\t\t\t\n\t\t\t\tRe: [花邊] 西河霸氣談比賽衝突：誰也別想動我隊友！\n\t\t\t\n\t\t\t
    ## 86                        \n\t\t\t\n\t\t\t\t(本文已被刪除) [BrandonMai]\n\t\t\t\n\t\t\t
    ## 87                \n\t\t\t\n\t\t\t\t[討論] Kevin Love的歷史定位會如何？\n\t\t\t\n\t\t\t
    ## 88       \n\t\t\t\n\t\t\t\tRe: [情報] 最愛哪個投籃？Curry：首次總決G5第\n\t\t\t\n\t\t\t
    ## 89   \n\t\t\t\n\t\t\t\tRe: [情報] R:Rondo召集08綠軍冠軍隊聚會，有人不想\n\t\t\t\n\t\t\t
    ## 90         \n\t\t\t\n\t\t\t\t[新聞] 季後賽機會渺茫 安東尼暗示恐離開尼克\n\t\t\t\n\t\t\t
    ## 91        \n\t\t\t\n\t\t\t\t[心得] 看了單場得分50+統計，原來老大這麼強!\n\t\t\t\n\t\t\t
    ## 92      \n\t\t\t\n\t\t\t\t[專欄] [李亦伸專欄] 過去兩季勇士回來了... LYS\n\t\t\t\n\t\t\t
    ## 93            \n\t\t\t\n\t\t\t\t[新聞] 被嘲笑沒關係 胡瓏貿：我有NBA夢想\n\t\t\t\n\t\t\t
    ## 94                        \n\t\t\t\n\t\t\t\tRe: [討論] 尼克怎麼這麼慘啊\n\t\t\t\n\t\t\t
    ## 95            \n\t\t\t\n\t\t\t\tRe: [討論] Kevin Love的歷史定位會如何？\n\t\t\t\n\t\t\t
    ## 96                \n\t\t\t\n\t\t\t\t[新聞] 看輪休爭議  Bosh：能打就該打\n\t\t\t\n\t\t\t
    ## 97        \n\t\t\t\n\t\t\t\tRe: [新聞] 被嘲笑沒關係 胡瓏貿：我有NBA夢想\n\t\t\t\n\t\t\t
    ## 98    \n\t\t\t\n\t\t\t\tRe: [心得] 看了單場得分50+統計，原來老大這麼強!\n\t\t\t\n\t\t\t
    ## 99                     \n\t\t\t\n\t\t\t\t[討論] 多次進明星賽VS得一次MVP\n\t\t\t\n\t\t\t
    ## 100       \n\t\t\t\n\t\t\t\tRe: [新聞] 被嘲笑沒關係 胡瓏貿：我有NBA夢想\n\t\t\t\n\t\t\t
    ##     PushNum       Author
    ## 1        76   FeiWenKing
    ## 2        40         Yui5
    ## 3        39 jailkobe5566
    ## 4                      -
    ## 5        50     nocturne
    ## 6        69    jimmy5680
    ## 7        21        xaima
    ## 8        爆    knic52976
    ## 9         8     avrild12
    ## 10       60   frank47147
    ## 11       30     gt097231
    ## 12           YuChEnChAnG
    ## 13       47        omare
    ## 14       54        otter
    ## 15       14    dragon803
    ## 16                sam369
    ## 17       27    checktime
    ## 18        8        Rambo
    ## 19       11     carotyao
    ## 20        7 iam168888888
    ## 21       68         Yui5
    ## 22       爆        Rambo
    ## 23       79         kart
    ## 24       80 johnnykao530
    ## 25       31     Miralles
    ## 26       36        Rambo
    ## 27       38        Rambo
    ## 28       X2            -
    ## 29       11    uuuuOPuff
    ## 30       22        c1236
    ## 31       51        Rambo
    ## 32       16    micbrimac
    ## 33       99    Turtle100
    ## 34       38     kadasaki
    ## 35        3    leo755269
    ## 36       43      firstsg
    ## 37                     -
    ## 38       X3     jhemezuo
    ## 39       20  JayFans0610
    ## 40       19   jay0601zzz
    ## 41       X6     zzyyxx77
    ## 42        8        Rambo
    ## 43       爆        Rambo
    ## 44       20    dragon803
    ## 45       17       eddman
    ## 46       爆        Rambo
    ## 47       爆      s106667
    ## 48       13        Rambo
    ## 49       32       pneumo
    ## 50       77      pttpepe
    ## 51        4        Max11
    ## 52       爆        Rambo
    ## 53       爆   jay0601zzz
    ## 54       11    dragon803
    ## 55       16        Rambo
    ## 56       10 Aretimis7345
    ## 57       19        Rambo
    ## 58       45        Rambo
    ## 59       83        Rambo
    ## 60        3     nba00077
    ## 61        2            -
    ## 62       36  Raskolnikov
    ## 63        7        slapt
    ## 64       36    kingtseng
    ## 65       18    rabbit529
    ## 66       42    ZaneTrout
    ## 67       19       kusami
    ## 68       32   bigDwinsch
    ## 69        1     marcus40
    ## 70       28       huntai
    ## 71       48   bigDwinsch
    ## 72       X1         rial
    ## 73       11   Levine0928
    ## 74        8            -
    ## 75       35       deehsu
    ## 76       38  ilovedandan
    ## 77       18        Rambo
    ## 78       46        Rambo
    ## 79        3        Rambo
    ## 80       27   thnlkj0665
    ## 81       37       s66449
    ## 82        7 PegasusSeiya
    ## 83       21     avrild12
    ## 84       49            -
    ## 85            sunnycello
    ## 86       X2            -
    ## 87       28    KevinLove
    ## 88       25 KyrieIrving1
    ## 89       31    pennylook
    ## 90       31      iso2288
    ## 91       68    checktime
    ## 92       X4  usa29574738
    ## 93       爆 iam168888888
    ## 94       13   carmeloeat
    ## 95               s106667
    ## 96       46   thnlkj0665
    ## 97       X2 KDimitrov313
    ## 98       15        arcss
    ## 99        7     BBDurant
    ## 100      X1 KDimitrov313

爬蟲結果呈現
------------

``` r
#這是R Code Chunk
##印出100則
knitr::kable(data[1:100,c("Title","PushNum","Author")]) ##請將iris取代為上個步驟中產生的爬蟲資料資料框
```

| Title                                               | PushNum | Author       |
|:----------------------------------------------------|:--------|:-------------|
| \[討論\] Klay Thompson 現役最強3D                   | 76      | FeiWenKing   |
| \[新聞\] 上場時間將大幅縮水 甜瓜：我能理解          | 40      | Yui5         |
| \[新聞\] 「俠客」銅像揭幕儀式 Kobe將出席共襄盛      | 39      | jailkobe5566 |
| (本文已被刪除) \[ZachLavine08\]                     |         | -            |
| Re: \[討論\] Klay Thompson 現役最強3D               | 50      | nocturne     |
| \[新聞\] 鬼之切入成絕響？ 吉諾比利：籃球已經不      | 69      | jimmy5680    |
| \[新聞\] 堅決反對輪休　湯普森父：打82場並不難       | 21      | xaima        |
| \[討論\] 現役球員誰的三重威脅做的最好               | 爆      | knic52976    |
| \[情報\] 表弟本季在國王與鵜鶘皆拿下單場40分         | 8       | avrild12     |
| \[討論\] 巴特勒是不是有什麼致命的缺點?              | 60      | frank47147   |
| \[新聞\] 杜蘭特恢復練投 傳季後賽前可望復出          | 30      | gt097231     |
| \[新聞\] 林書豪腳傷恐先發不保？                     |         | YuChEnChAnG  |
| \[討論\] Klay Thompson &Ray Allen三分投籃姿勢       | 47      | omare        |
| \[討論\] 製造進攻犯規的高手?                        | 54      | otter        |
| Re: \[討論\] 製造進攻犯規的高手?                    | 14      | dragon803    |
| Re: \[討論\] 巴特勒是不是有什麼致命的缺點?          |         | sam369       |
| \[討論\] 美國史上最弱奧運男籃隊-2004雅典奧運        | 27      | checktime    |
| \[情報\] ★今日排名(2017.03.22)★                     | 8       | Rambo        |
| Re: \[討論\] 製造進攻犯規的高手?                    | 11      | carotyao     |
| \[新聞\] 兄弟同場較勁 咖哩哥面子、裡子都占上風      | 7       | iam168888888 |
| \[情報\] O'Neal：尼克球員的壞習慣毀掉了三角進攻     | 68      | Yui5         |
| \[BOX \] Warriors 112:87 Mavericks 數據             | 爆      | Rambo        |
| Re: \[新聞\] 詹姆斯抱怨：我只休2場 馬刺用了15年     | 79      | kart         |
| \[新聞\] Lebron James warning Larva Ball            | 80      | johnnykao530 |
| Re: \[新聞\] NBA╱小牛老闆建議 延長賽季時間          | 31      | Miralles     |
| \[BOX \] Spurs 100:93 Timberwolves 數據             | 36      | Rambo        |
| \[BOX \] Bucks 93:90 Blazers 數據                   | 38      | Rambo        |
| (本文已被刪除) \[sunyeah\]                          | X2      | -            |
| Re: \[新聞\] NBA╱小牛老闆建議 延長賽季時間          | 11      | uuuuOPuff    |
| Re: \[心得\] 看了單場得分50+統計，原來老大這麼強!   | 22      | c1236        |
| \[BOX \] Clippers 133:109 Lakers 數據               | 51      | Rambo        |
| Re: \[新聞\] 詹姆斯抱怨：我只休2場 馬刺用了15年     | 16      | micbrimac    |
| Re: \[新聞\] 詹姆斯抱怨：我只休2場 馬刺用了15年     | 99      | Turtle100    |
| \[情報\] NBA Standings(2017.03.22)                  | 38      | kadasaki     |
| Re: \[新聞\] 詹姆斯抱怨：我只休2場 馬刺用了15年     | 3       | leo755269    |
| \[花邊\] LBJ警告球爸別談論他兒子 球爸表示被斷章     | 43      | firstsg      |
| (本文已被刪除) \[wmigrant\]                         |         | -            |
| \[新聞\] 火氣太大了5天內3起群毆　有錢球員太任性     | X3      | jhemezuo     |
| Re: \[新聞\] 詹姆斯抱怨：我只休2場 馬刺用了15年     | 20      | JayFans0610  |
| \[情報\] Hassan Whiteside右手受傷                   | 19      | jay0601zzz   |
| \[專欄\] 球員無限制輪休 早晚會被球迷抵制LYS         | X6      | zzyyxx77     |
| \[Live\] 灰熊 @ 鵜鶘                                | 8       | Rambo        |
| \[Live\] 勇士 @ 小牛                                | 爆      | Rambo        |
| \[情報\] Milos Teodosic談加入NBA的可能性            | 20      | dragon803    |
| Re: \[討論\] 輪休到底對NBA是利還是弊？              | 17      | eddman       |
| \[Live\] 馬刺 @ 灰狼                                | 爆      | Rambo        |
| \[情報\] Kobe-NBA唯一個對所有球隊40+的男人          | 爆      | s106667      |
| \[Live\] 公鹿 @ 拓荒者                              | 13      | Rambo        |
| \[新聞\] 波波維奇有個性 不甩聯盟警告繼續輪休        | 32      | pneumo       |
| \[新聞\] 詹姆斯抱怨：我只休2場 馬刺用了15年         | 77      | pttpepe      |
| Re: \[討論\] 輪休到底對NBA是利還是弊？              | 4       | Max11        |
| \[BOX \] Pistons 96:98 Nets 數據                    | 爆      | Rambo        |
| \[花邊\] Lopez與Ibaka發生衝突                       | 爆      | jay0601zzz   |
| \[閒聊\] Udonis Haslem跟Spoelstra談球隊防守         | 11      | dragon803    |
| \[Live\] 快艇 @ 湖人                                | 16      | Rambo        |
| Re: \[討論\] 輪休到底對NBA是利還是弊？              | 10      | Aretimis7345 |
| \[BOX \] Suns 97:112 Heat 數據                      | 19      | Rambo        |
| \[BOX \] Bulls 120:122 Raptors 數據                 | 45      | Rambo        |
| \[BOX \] Grizzlies 82:95 Pelicans 數據              | 83      | Rambo        |
| \[討論\] KD何時會歸隊??                             | 3       | nba00077     |
| (本文已被刪除) \[MrSatan\]                          | 2       | -            |
| Re: \[新聞\] 被嘲笑沒關係 胡瓏貿：我有NBA夢想       | 36      | Raskolnikov  |
| \[情報\] Hayward拿下生涯新高38分 爵士輸球           | 7       | slapt        |
| \[新聞\] 球星輪休爭議多 聯盟出手管了                | 36      | kingtseng    |
| \[情報\] NBA Power Rankings 3/20(官網)              | 18      | rabbit529    |
| Fw: \[問卦\]體育界跨領域超強三兄弟                  | 42      | ZaneTrout    |
| \[情報\] 金塊總教練談Harden不輪休                   | 19      | kusami       |
| \[花邊\] 馬刺Green談為何養蛇：看他們進食很過癮      | 32      | bigDwinsch   |
| \[討論\] kd受傷會成就可怕勇士誕生嗎？               | 1       | marcus40     |
| Re: \[心得\] 看了單場得分50+統計，原來老大這麼強!   | 28      | huntai       |
| \[情報\] Curry：要弄清如何限制弟弟的發揮            | 48      | bigDwinsch   |
| Re: \[新聞\] 被嘲笑沒關係 胡瓏貿：我有NBA夢想       | X1      | rial         |
| \[徵求\]03/21 12點至1點高鐵總機廠前行車紀錄畫面     | 11      | Levine0928   |
| (本文已被刪除) \[CGary\]                            | 8       | -            |
| Fw: \[情報\] 小威 & Stephen Curry 兵乓球之戰        | 35      | deehsu       |
| \[外絮\] Jerry Krause 過世                          | 38      | ilovedandan  |
| \[Live\] 公牛 @ 暴龍                                | 18      | Rambo        |
| \[Live\] 活塞 @ 籃網                                | 46      | Rambo        |
| \[Live\] 太陽 @ 熱火                                | 3       | Rambo        |
| \[情報\] 林書豪將缺席今天對活塞隊的比賽             | 27      | thnlkj0665   |
| \[情報\] 最愛哪個投籃？Curry：首次總決G5第四節      | 37      | s66449       |
| Re: \[情報\] Rondo召集08綠軍冠軍隊聚會，有人不想All | 7       | PegasusSeiya |
| \[情報\] Harden連續3場35分10助攻                    | 21      | avrild12     |
| (本文已被刪除) \[MrSatan\]                          | 49      | -            |
| Re: \[花邊\] 西河霸氣談比賽衝突：誰也別想動我隊友！ |         | sunnycello   |
| (本文已被刪除) \[BrandonMai\]                       | X2      | -            |
| \[討論\] Kevin Love的歷史定位會如何？               | 28      | KevinLove    |
| Re: \[情報\] 最愛哪個投籃？Curry：首次總決G5第      | 25      | KyrieIrving1 |
| Re: \[情報\] R:Rondo召集08綠軍冠軍隊聚會，有人不想  | 31      | pennylook    |
| \[新聞\] 季後賽機會渺茫 安東尼暗示恐離開尼克        | 31      | iso2288      |
| \[心得\] 看了單場得分50+統計，原來老大這麼強!       | 68      | checktime    |
| \[專欄\] \[李亦伸專欄\] 過去兩季勇士回來了... LYS   | X4      | usa29574738  |
| \[新聞\] 被嘲笑沒關係 胡瓏貿：我有NBA夢想           | 爆      | iam168888888 |
| Re: \[討論\] 尼克怎麼這麼慘啊                       | 13      | carmeloeat   |
| Re: \[討論\] Kevin Love的歷史定位會如何？           |         | s106667      |
| \[新聞\] 看輪休爭議 Bosh：能打就該打                | 46      | thnlkj0665   |
| Re: \[新聞\] 被嘲笑沒關係 胡瓏貿：我有NBA夢想       | X2      | KDimitrov313 |
| Re: \[心得\] 看了單場得分50+統計，原來老大這麼強!   | 15      | arcss        |
| \[討論\] 多次進明星賽VS得一次MVP                    | 7       | BBDurant     |
| Re: \[新聞\] 被嘲笑沒關係 胡瓏貿：我有NBA夢想       | X1      | KDimitrov313 |

解釋爬蟲結果
------------

``` r
#這是R Code Chunk
nrow(data)
```

    ## [1] 100

nrow() 用來算列數，得到100列，所以可以知道包含被刪掉的標題共爬出100篇文章

``` r
#這是R Code Chunk
table(data$Author)
```

    ## 
    ##            -     avrild12     carotyao    checktime    dragon803 
    ##            7            2            1            2            3 
    ##   FeiWenKing   frank47147     gt097231 iam168888888 jailkobe5566 
    ##            1            1            1            2            1 
    ##    jimmy5680    knic52976     nocturne        omare        otter 
    ##            1            1            1            1            1 
    ##        Rambo       sam369        xaima  YuChEnChAnG         Yui5 
    ##           17            1            1            1            2 
    ##        c1236      firstsg   jay0601zzz  JayFans0610     jhemezuo 
    ##            1            1            2            1            1 
    ## johnnykao530     kadasaki         kart    leo755269    micbrimac 
    ##            1            1            1            1            1 
    ##     Miralles    Turtle100    uuuuOPuff Aretimis7345       eddman 
    ##            1            1            1            1            1 
    ##        Max11     nba00077       pneumo      pttpepe      s106667 
    ##            1            1            1            1            2 
    ##     zzyyxx77   bigDwinsch       deehsu       huntai  ilovedandan 
    ##            1            2            1            1            1 
    ##    kingtseng       kusami   Levine0928     marcus40    rabbit529 
    ##            1            1            1            1            1 
    ##  Raskolnikov         rial        slapt   thnlkj0665    ZaneTrout 
    ##            1            1            1            2            1 
    ##        arcss     BBDurant   carmeloeat      iso2288 KDimitrov313 
    ##            1            1            1            1            2 
    ##    KevinLove KyrieIrving1 PegasusSeiya    pennylook       s66449 
    ##            1            1            1            1            1 
    ##   sunnycello  usa29574738 
    ##            1            1

可以看到table中，有個作者叫Rambo 一共發了17則推文，是裡面發文數最多的人

心得: 我覺得NBA的文章都挺無聊的，可能因為我本身不太FOLLOW籃球，隨意點了幾則推文數爆的進去看，發現大家只是在閒聊或是分享看比賽心得，而且通常那些文章都是新聞或是LIVE的影片分享，對我來說，還是八卦版之類的版有趣一點
