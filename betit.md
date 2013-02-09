betit
====================================
（新增接口）

版本：0.1  
作者：[钟魏](mailto:623610577@qq.com)

本文档用于描述betit的客户端接口  
2013.1.30  进行修复和新增了一些接口   
 
************************************

索引
----
* 接口
       *      [删除功能接口](#删除功能接口)
	   *      [竞猜转发功能接口](#竞猜转发功能接口)
	   *      [搜索相片接口](#搜索相片接口)
	   *      [我的相册接口](#我的相册接口)
	   *      [即将开奖功能接口](#即将开奖功能接口)
	   *      [编辑功能接口](#编辑功能接口)
	   *      [用户推荐接口](#用户推荐接口)
	   *      [发布竞猜ajax提示接口](#发布竞猜ajax提示接口)


<h2>删除功能接口</h2>


域名/capi/cp.php?ac=quiz&op=delete&quizid=671&deletesubmit=true&m_auth=d818Swk1yNhoy5rOqipzumWwftKZveHszvob4Xz40FGEm3WenlarXw2BkoafJ07MMt0TRZaCVX8CQJk0IUNb
  
####请求参数

>     * 要删除的竞猜ID--quizid 
>     * 操作类型（固定搭配）--deletesubmit:true,op:delete
>     * API密钥--m_auth,每次调用接口，需要提供此Key以验证用户

####返回参数  
>     * 错误码--code,0:代表成功,1:代表失败 
>     * 错误类型--action, login_success:代表登录成功
>     * 错误信息 -- msg, 详细参见附录
>     * 结果 -- data, 删除成功后跳转的地址
>         * space.php?uid=1&do=quiz&view=me  

####样例
>       ｛
>        "code": 0  
>        "data":     
>            "space.php?uid=1&do=quiz&view=me" 
>        "msg": "进行的操作完成了"  
>        "action": "do_success"  
       }

[↑返回顶部](#betit)  

<h2>竞猜转发功能接口</h2>
域名/capi/cp.php?ac=quiz&fquizid=668&makefeed=ture&quizsubmit=true&subject=我的打赌&options[1]=A赢&options[2]=B输&pics[1]=81&pics[2]=79&joincost=20&portion=3 &endtime=12324324235&resulttime=4343234&friend=0&m_auth=ff8cf2wDkUUiu8syK%2BP1DgK6j5n79FLSYfgtW%2FEIMkM514wfowT6ABYChlTA%2BrpgDA6QwEkBkzXOkVRONoSX

####请求参数  

>     * 操作类型（固定搭配）--quizsubmit:true 
>     * 是否发布动态--makefeed:true
>     * 打赌的标题 -- subject
>     * A选项的描述 -- options[1]
>     * B选项的描述 -- options[2]
>     * A选项的图片id -- pics[1]
>     * B选项的图片id -- pics[2]
>     * 每一份投注需要的金币数 -- joincost
>     * 每个用户可允许的最大投注次数 -- portion
>     * 打赌投注截止时间 -- endtime
>     * 打赌预计公布答案时间 -- resulttime
>     * 是否全站公开 -- frined , 默认0全站公开
>     * 转发竞猜所转发的原竞猜ID -- fquizid , 默认0全站公开  

####返回参数
  
>     * 错误码--code,0:代表成功,1:代表失败 
>     * 错误类型--action, login_success:代表登录成功
>     * 错误信息 -- msg, 详细参见附录
>     * 结果 -- data, json数组, 本操作返回一个数据
>     	  * data[quiz] -- 发布成功的打赌，具体条目如下:
>         * 打赌的标题 -- subject
>         * 是否全站公开 -- frined , 默认0全站公开
>         * 每一份投注需要的金币数 -- joincost
>         * 每个用户可允许的最大投注次数 -- portion
>         * 打赌投注截止时间 -- endtime
>         * 打赌预计公布答案时间 -- resulttime
>         * 打赌id --  quizid
>         * 发布的用户id -- uid
>         * 发布的用户名 -- username
>         * reward -- 操作增加的金币分和经验
>            * credit -- 金币
>            * experience -- 经验 
>         * 转发原竞猜id--fquizid   

####样例
>        ｛   
       "code": 0,  
       "data": {  
          "quiz": {  
            "subject": "我的打赌",  
            "classid": 0,  
            "friend": 0,  
            "password": null,  
            "noreply": 0,  
            "joincost": 20,  
            "portion": 3,  
            "endtime": 2147483647,  
            "resulttime": 4343234,  
            "picflag": 0,  
            "pic": "",  
            "hot": 0,  
            "topicid": 0,  
            "uid": 1,  
            "username": "admin",  
            "dateline": "1358947862",  
            "quizid": 701,  
            "reward": {  
                 "credit": 0,  
                "experience": 0  
            },  
            "fquizid": 668  
        }  
    },  
    "msg": "进行的操作完成了",  
    "action": "do_success"  
}

[↑返回顶部](#betit)  

<h2>搜索相片接口</h2>
域名/capi/space.php?searchkey=3&searchsubmit=搜索相册&do=album&page=0&perpage=2&view=all&orderby=dateline&m_auth=ff8cf2wDkUUiu8syK%2BP1DgK6j5n79FLSYfgtW%2FEIMkM514wfowT6ABYChlTA%2BrpgDA6QwEkBkzXOkVRONoSX

####请求参数
>     * 第几页--page
>     * 每页显示数量--perpage
    * 查询参数 -- view, 必须为all
    * 查询内容 -- searchkey
    * 操作类型（固定搭配）--searchsubmit:搜索相册，orderby：dateline
    * API密钥 -- m_auth, 由登录后返回

####返回字段
>     * 错误码 -- code, 0:代表成功， 1:代表失败
    * 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
    * 错误信息 -- msg, 详细参见附录
    * 结果 -- data, json数组, 本操作返回三个数据
    * data[quizs]，打赌列表， 条目字段如下
       * 搜索图片id："picid"
       * 搜索图片对应相册id："albumid"
	   * 搜索图片地址："pic"
    * data[count], 返回列表条目数, 便用遍历
    * data[reward], 查询操作扣除的金币和信用

####样例
>     {
    "code": 0,
    "data": {
        "quizs": [
            {
                "picid": "79",
                "albumid": "0",
                "pic": "http://betit-pic.b0.upaiyun.com/201208/1/1_1343816747cmwS.png"
            },
            {
                "picid": "78",
                "albumid": "0",
                "pic": "http://betit-pic.b0.upaiyun.com/201208/1/1_1343816737ECth.png"
            }
        ],
        "count": 2,
        "reward": null
    },
    "msg": "数据获取成功",
    "action": "rest_success"
}
  
[↑返回顶部](#betit) 

<h2>我的相册接口</h2>
域名/capi/space.php?uid=1&do=album&view=me&page=0&perpage=2&orderby=dateline&queryop=up&dateline=1343793316&m_auth=1e49Ty2YF1kd3wZAF1eyULPpkE9lqtWyWzUTbPZfrus4lM3lGtbmQp8pmB6X68L4o%2FC799tJ4o%2BKCDWcWn3V

####请求参数
>     * 第几页--page
>     * 每页显示数量--perpage
    * 查询参数 -- view, me为我的相册，we为好友最新相册，all为大家的相册，click为我表态过的图片
    * API密钥 -- m_auth, 由登录后返回
    * 时间点 -- dateline
    * 查询方式 -- queryop, 取值可以是up, down
       * up 代表上拉，取比dateline新的打赌
       * down 代表到底，取紧接着dateline之后的打赌

####返回字段
>     * 错误码 -- code, 0:代表成功， 1:代表失败
    * 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
    * 错误信息 -- msg, 详细参见附录
    * 结果 -- data, json数组, 本操作返回三个数据
    * data[quizs]，打赌列表， 条目字段如下
       * 相册id："albumid"
       * 相册名字："albumname"
	   * 发布相册时间："dateline"
       * 更新时间："updatetime"
    * data[count], 返回列表条目数, 便用遍历

####样例
>     {
    "code": 0,
    "data": {
        "quizs": [
            {
                "albumid": "2",
                "albumname": "shne",
                "uid": "1",
                "username": "admin",
                "dateline": "1357741664",
                "updatetime": "1357741664",
                "picnum": "0",
                "pic": "image/nopic.gif",
                "picflag": "0",
                "friend": "0",
                "password": "",
                "target_ids": ""
            }
        ],
        "count": 1
    },
    "msg": "数据获取成功",
    "action": "rest_success"
} 
 
[↑返回顶部](#betit) 


<h2>即将开奖功能接口</h2>
域名/capi/space.php?do=feed&view=open&queryop=up&m_auth=ff8cf2wDkUUiu8syK%2BP1DgK6j5n79FLSYfgtW%2FEIMkM514wfowT6ABYChlTA%2BrpgDA6QwEkBkzXOkVRONoS  



####请求参数  

>     * 查询参数--view，值为open代表即将开奖动态列表 
>     * API密钥 -- m_auth, 由登录后返回

####返回字段
>     * 错误码 -- code, 0:代表成功， 1:代表失败
    * 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
    * 错误信息 -- msg, 详细参见附录
    * 结果 -- data, json数组, 本操作返回三个数据
    * data[feeds]，打赌列表， 条目字段如下
       * 用户id--uid
       * 竞猜发布时间--dateline
	   * 竞猜标题--subject
       * 选项oid--option[oid]
       * 选项名称--option[option]
	   * 投此选项票的数量--option[votenum]
	   * 投此选项票的时间--option[relatedtime]
	   * 选项图片--option[pic]
	   * 竞猜总金币--totalcost
	   * 竞猜截止时间--endtime
	   * 竞猜公布答案时间--resulttime
       * 竞猜id--id
    * data[count], 返回列表条目数, 便用遍历
    * data[reward], 查询操作扣除的金币和信用

####样例
>     {
    "code": 0,
    "data": {
        "feeds": [
            {
                "uid": "1",
                "username": "admin",
                "hot": "0",
                "dateline": "1358997653",
                "friend": "0",
                "icon": "quiz",
                "title_template": "{actor}:<b>{subject}</b>",
                "title_data": {
                    "subject": "23424",
                    "actor": "admin"
                },
                "body_template": "quiz",
                "body_data": {
                    "option": [
                        {
                            "oid": "1321",
                            "option": "345345",
                            "relatedtime": "1358997653",
                            "votenum": "0",
                            "pic": ""
                        },
                        {
                            "oid": "1322",
                            "option": "2424",
                            "relatedtime": "1358997653",
                            "votenum": "0",
                            "pic": ""
                        }
                    ],
                    "subject": "23424",
                    "totalcost": "0",
                    "endtime": "1358998200",
                    "resulttime": "1359085800",
                    "hasexceed": 0,
                    "keyoid": "0"
                },
                "id": "705",
                "idtype": "quizid",
                "avatar": "http://localhost/uchome/betit/center/images/noavatar_small.gif",
                "isonline": ""
            }
        ],
        "count": 1
    },
    "msg": "数据获取成功",
    "action": "rest_success"
}    

[↑返回顶部](#betit)

<h2>编辑功能接口</h2>
域名/capi/cp.php?uid=1&ac=quiz&quizid=670&quizsubmit=true&subject=我的打赌&options[1]=A赢&options[2]=B输&pics[1]=81&pics[2]=79&joincost=20&portion=3 &endtime=12324324235&resulttime=4343234&friend=0&m_auth=ff8cf2wDkUUiu8syK%2BP1DgK6j5n79FLSYfgtW%2FEIMkM514wfowT6ABYChlTA%2BrpgDA6QwEkBkzXOkVRONoSX

####请求参数  

>     * 操作类型（固定搭配）--quizsubmit：true
>     * API密钥 -- m_auth, 由登录后返回
>     * 所编辑竞猜id -- quizid

####返回字段
>     * 错误码 -- code, 0:代表成功， 1:代表失败
    * 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
    * 错误信息 -- msg, 详细参见附录
    * 结果 -- data, json数组
    * data[quiz]如下
       * 竞猜标题--subject
       * 每一份投注需要的金币数 -- joincost
	   * 每个用户可允许的最大投注次数 -- portion
       * 打赌投注截止时间 -- endtime
       * 打赌预计公布答案时间 -- resulttime
	   * A选项的描述 -- options[1]
	   * B选项的描述 -- options[2]
	   * A选项的图片id -- pics[1]
	   * B选项的图片id -- pics[2]
	   * 竞猜截止时间--endtime
	   * 是否全站公开 -- frined , 默认0全站公开

####样例
>     {
    "code": 0,
    "data": {
        "quiz": {
            "subject": "我的打赌",
            "classid": 0,
            "friend": 0,
            "password": null,
            "noreply": 0,
            "joincost": 20,
            "portion": 3,
            "endtime": 2147483647,
            "resulttime": 4343234,
            "picflag": 0,
            "pic": "",
            "hot": 0,
            "topicid": 0,
            "uid": 1,
            "username": "admin",
            "dateline": "1359001247",
            "quizid": 707,
            "reward": {
                "credit": 0,
                "experience": 0
            }
        }
    },
    "msg": "进行的操作完成了",
    "action": "do_success"
}  

[↑返回顶部](#betit)


<h2>用户推荐接口</h2>

域名/capi/space.php?do=top&view=online&page=0&perpage=2&m_auth=1e49Ty2YF1kd3wZAF1eyULPpkE9lqtWyWzUTbPZfrus4lM3lGtbmQp8pmB6X68L4o%2FC799tJ4o%2BKCDWcWn3V  
####请求参数  

>     * 查询参数--view，值为online代表在线用户 
>     * API密钥 -- m_auth, 由登录后返回

####返回字段
>     * 错误码 -- code, 0:代表成功， 1:代表失败
    * 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
    * 错误信息 -- msg, 详细参见附录
    * 结果 -- data, json数组
    * data[top]如下
       * 用户id--uid
       * 用户组id -- groupid
	   * 用户名 -- username
       * 用户实名 -- name
       
####样例

>     {
    "code": 0,
    "data": {
        "top": {
            "28": {
                "uid": "28",
                "groupid": "10",
                "credit": "1369998765",
                "experience": "911",
                "username": "wei",
                "name": "钟魏",
                "namestatus": "1",
                "videostatus": "0",
                "domain": "",
                "friendnum": "0",
                "viewnum": "102",
                "notenum": "0",
                "addfriendnum": "0",
                "mtaginvitenum": "0",
                "eventinvitenum": "0",
                "myinvitenum": "0",
                "pokenum": "0",
                "doingnum": "24",
                "blognum": "8",
                "albumnum": "0",
                "threadnum": "1",
                "pollnum": "1",
                "eventnum": "1",
                "sharenum": "0",
                "dateline": "1350970129",
                "updatetime": "1359699421",
                "lastsearch": "1358147430",
                "lastpost": "1359699421",
                "lastlogin": "1359696994",
                "lastsend": "0",
                "attachsize": "5578100",
                "addsize": "0",
                "addfriend": "0",
                "flag": "0",
                "newpm": "0",
                "avatar": "0",
                "regip": "127.0.0.1",
                "ip": "127000000",
                "mood": "0",
                "quiznum": "143",
                "winnum": "10",
                "lostnum": "1",
                "voternum": "38",
                "sex": "1",
                "email": "wei@betit.cn",
                "newemail": "",
                "emailcheck": "0",
                "mobile": "",
                "qq": "",
                "msn": "",
                "msnrobot": "",
                "msncstatus": "0",
                "videopic": "",
                "birthyear": "0",
                "birthmonth": "0",
                "birthday": "0",
                "blood": "",
                "marry": "0",
                "birthprovince": "",
                "birthcity": "",
                "resideprovince": "",
                "residecity": "",
                "note": "2",
                "spacenote": "坑大跌",
                "authstr": "",
                "theme": "",
                "nocss": "0",
                "menunum": "0",
                "css": "",
                "privacy": "",
                "friend": "",
                "feedfriend": "",
                "sendmail": "",
                "magicstar": "0",
                "magicexpire": "0",
                "timeoffset": "",
                "weibo": ""
            }
        }
    },
    "msg": "数据获取成功",
    "action": "rest_success"
}


[↑返回顶部](#betit)

<h2>发布竞猜ajax提示接口</h2>
域名/capi/space.php?do=ajax&keywords=2&page=0&perpage=2&m_auth=d818Swk1yNhoy5rOqipzumWwftKZveHszvob4Xz40FGEm3WenlarXw2BkoafJ07MMt0TRZaCVX8CQJk0IUNb 

####请求参数  

>     * 查询参数--keywords，为发布竞猜标题
>     * API密钥 -- m_auth, 由登录后返回

####返回字段

>     * 错误码 -- code, 0:代表成功， 1:代表失败
    * 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
    * 错误信息 -- msg, 详细参见附录
    * 结果 -- data, json数组
    * data[]如下
       * 竞猜标题--subject
       * 转发的原竞猜id -- fquizid
	   * 选项A的oid -- option[oid]
	   * 选项A的值 -- option[option]
       * 投选项A的票的值 -- option[votenum]
       * 选项A的图片的地址 -- option[pic]
	   * 选项B的oid -- option[oid]
	   * 选项B的值 -- option[option]
       * 投选项B的票的值 -- option[votenum]
       * 选项B的图片的地址 -- option[pic]

####样例
>      {
    "code": 0,
    "data": [
        {
            "quizid": "47",
            "uid": "1",
            "tag": "",
            "message": "",
            "postip": "127.0.0.1",
            "related": "",
            "relatedtime": "0",
            "target_ids": "",
            "hotuser": "",
            "magiccolor": "0",
            "magicpaper": "0",
            "magiccall": "0",
            "option": "a:2:{i:0;s:3:\"234\";i:1;s:3:\"234\";}",
            "invite": "",
            "topicid": "0",
            "username": "admin",
            "subject": "234",
            "classid": "0",
            "viewnum": "0",
            "replynum": "0",
            "hot": "0",
            "dateline": "1343966557",
            "pic": "",
            "picflag": "0",
            "noreply": "0",
            "friend": "0",
            "password": "",
            "click_1": "0",
            "click_2": "0",
            "click_3": "0",
            "click_4": "0",
            "click_5": "0",
            "joincost": "100",
            "portion": "3",
            "endtime": "1343966566",
            "resulttime": "1344574953",
            "lastvote": "1343966561",
            "voternum": "1",
            "maxchoice": "0",
            "sex": "0",
            "keyoid": "3",
            "keyoption": "",
            "totalcost": "100",
            "hasremind": "1",
            "hasexceed": "0",
            "fquizid": "359",
            "id": "0",
            "options": [
                {
                    "oid": "91",
                    "quizid": "47",
                    "uid": "1",
                    "option": "234",
                    "relatedtime": "1343966557",
                    "picid": "0",
                    "votenum": "1"
                },
                {
                    "oid": "92",
                    "quizid": "47",
                    "uid": "1",
                    "option": "234",
                    "relatedtime": "1343966557",
                    "picid": "0",
                    "votenum": "0"
                }
            ]
        },
        {
            "quizid": "56",
            "uid": "1",
            "tag": "",
            "message": "",
            "postip": "127.0.0.1",
            "related": "",
            "relatedtime": "0",
            "target_ids": "",
            "hotuser": "",
            "magiccolor": "0",
            "magicpaper": "0",
            "magiccall": "0",
            "option": "a:2:{i:0;s:2:\"21\";i:1;s:3:\"123\";}",
            "invite": "",
            "topicid": "0",
            "username": "admin",
            "subject": "20120803时间戳",
            "classid": "0",
            "viewnum": "2",
            "replynum": "0",
            "hot": "0",
            "dateline": "1344929249",
            "pic": "",
            "picflag": "0",
            "noreply": "0",
            "friend": "0",
            "password": "",
            "click_1": "0",
            "click_2": "0",
            "click_3": "0",
            "click_4": "0",
            "click_5": "0",
            "joincost": "20",
            "portion": "3",
            "endtime": "1345533855",
            "resulttime": "1345537455",
            "lastvote": "0",
            "voternum": "0",
            "maxchoice": "0",
            "sex": "0",
            "keyoid": "0",
            "keyoption": "",
            "totalcost": "0",
            "hasremind": "1",
            "hasexceed": "1",
            "fquizid": "359",
            "id": "0",
            "options": [
                {
                    "oid": "109",
                    "quizid": "56",
                    "uid": "1",
                    "option": "21",
                    "relatedtime": "1344929249",
                    "picid": "91",
                    "votenum": "0",
                    "pic": "http://betit-pic.b0.upaiyun.com/201208/14/1_13449290756gK5.jpg!210x210"
                },
                {
                    "oid": "110",
                    "quizid": "56",
                    "uid": "1",
                    "option": "123",
                    "relatedtime": "1344929249",
                    "picid": "92",
                    "votenum": "0",
                    "pic": "http://betit-pic.b0.upaiyun.com/201208/14/1_1344929111K4Ac.png!210x210"
                }
            ]
        }
    ],
    "msg": "数据获取成功",
    "action": "rest_success"
}
	


[↑返回顶部](#betit)