世界波API调用文档
===============

用户模块
--------

===获取用户资料√√（需更改，参看文档）
~~~~~~~~~~~~~
备注：在之前基础上删除honor和skill下的star字段，假如admin字段(已处理)

描述：根据UID获取用户资料(只能获取自己的) 

地址：/api/user/getprofile/

HTTP请求方式：GET

参数：
	* token，用户标识, 非空

返回数据：
::
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功,返回下述参数)
		data: 
		{
		    id: 123
		    nickname: "pubgeek"(昵称)
		    email: "admin@pubgeek.com"
		    avatar: "http://www.pubgeek.com/avatar/123"
		    sex: 1 (0 -- 女性，1 -- 男性)
		    height: 183 (身高)
		    weight: 75 (体重，单位为公斤)
		    birthday: 1234324241 (时间戳格式)
		    age: 21 (根据当前时间戳和birthday的时间戳来算年龄)
		    province: "北京"
		    city: "北京"
		    competitions:
		    [{
		    	time: 1234324241 (比赛时间，时间戳格式)
		    	place: "北京市海淀区北京理工大学" (比赛地点)
		    } ...]
		    level: 3 (用户现有等级)
		    exps: 123 (用户经验)
            skill:
            {
                passing:0,
                shooting:0,
                sense:0,
                physical:0,
                tech:0
            }
            team:
            [{
                'tid':1,
                'teamname':'test',
                'isadmin': true or false
             },{}
            ]
		}
	}

===更新用户资料√√√
~~~~~~~~~~~~~
描述：更新用户资料(已更新)

地址：/api/user/updateprofile/

HTTP请求方式：POST

参数：
	* name, 昵称, 非空
	* sex (0--男性，1--女性, 2--保密), 性别, 非空
	* birthday, 生日, 非空
	* height, 身高, 非空
	* weight, 体重, 非空
	* position, 场上位置, 非空, String类型
	* tid, 球队ID, 可为空
	* location, 位置信息，住址之类, 可为空 
	* token, 当前用户标识, 非空 

返回数据：
::
	{
		status: 0 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		error: "Network Error!"
	}

===创建球队√√（需更改，参看文档）
~~~~~~~~~~~~~
备注：在之前基础上删除latitude、longitude、owner字段，加入avatar、contact、phone字段

描述：创建球队

地址：/api/team/createteam/

HTTP请求方式：POST

参数：
	* avatar, 球队头像, 文件类型, 非空
	* fullname, 球队全称, 非空
	* shortname, 球队简称, 非空
	* introduction, 简介, 非空
	* home, 球场ID, 非空
	* members, 球员数目, 非空
	* contact, 联系人, 非空,非球员，随便填写
	* phone, 联系人电话, 非空
	* sponsor, 赞助商, 可为空
	* captain, 队长, 非空(必须从球员里选)
	* token, 当前用户标识, 非空

返回数据：
::
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		{
			tid: 12 (球队ID)
		}
	}


===更新用户地理位置√√√
~~~~~~~~~~~~~~~~~~~~
描述：更新用户地理位置

地址：/api/user/updatelocation/

HTTP请求方式：POST

参数：
	* latitude, 经度, 非空
	* longitude, 纬度, 非空
	* token, 当前用户标识, 非空 

返回数据：
::
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		{
			id: 12 (球队ID)
		}
	}

===更新用户头像√√√
~~~~~~~~~~~~~~~~~~~~
描述：更新用户头像

地址：/api/user/updateavatar/

HTTP请求方式：POST

参数：
	* avatar, 图片文件, 非空
	* token, 当前用户标识, 非空 
返回数据：
::
	{
		status: 0 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		error: "Network Error!"
	}


添加/删除朋友
~~~~~~~~~~~~~~~~~~~~
描述：添加朋友

地址：/api/user/friend/

HTTP请求方式：POST

参数：
	* uid, 对方用户id, 非空
	* token, 当前用户标识, 非空 
    * type, 操作，add 或 del
返回数据：
::
	{
		status: 0 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		error: "Network Error!"
	}


添加/删除球员(相对于球队)
~~~~~~~~~~~~~~~~~~~~
描述：添加/删除球员

地址：/api/team/team/

HTTP请求方式：POST

参数：
	* token, 当前用户标识, 非空 
    * uid, 待删除或者添加的球员id
	* tid, 球队id, 非空
    * type, 操作，add 或 del
返回数据：
::
	{
		status: 0 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功),
		error: "Network Error!"
	}


获取朋友列表
~~~~~~~~~~~~~~~~~~~~
描述：获取朋友列表

地址：/api/user/getfriends/

HTTP请求方式：POST

参数：
	* token, 当前用户标识, 非空 
返回数据：
::
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		[{
			id: 12 (球员ID)
			name: "世界波"
			avatar: "http://XXX.com/field/12.jpg"  (图片URL)
			height: "183" (身高)
			weight: "65" (体重)
			position: "前锋" (球队角色) 
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		}...]
	}


帐号模块
-------- 
===登录√√√
~~~~~~~~~~~~~
描述：登录

地址：/api/user/login/

HTTP请求方式：POST

参数：
	* username, 用户名/邮箱, 非空
	* password, 密码, 非空 

返回数据：
::
	{
		status: 0 (0 -- 请求失败, 返回error参数, 带上错误原因；1 -- 请求成功, 带上下述参数)
		token: 123fdesa324fea23
	}

===登出√√√
~~~~~~~~~~~~~
描述：登出

地址：/api/user/logout/

HTTP请求方式：POST

参数：
	* token, 当前用户标识, 非空

返回数据：
::
	{
		status: 0 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		error: "Network Error!"
	}

===修改密码√√√
~~~~~~~~~~~~~
描述：修改密码

地址：/api/user/changepassword/

HTTP请求方式：POST

参数：
	* old_password, 老密码, 非空
	* new_password1, 新密码, 非空
	* new_password2, 新密码确认, 非空
	* token, 当前用户标识, 非空

返回数据：
::
	{
		status: 0 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		error: "Network Error!"
	}

发送重置密码邮件至指定邮箱
~~~~~~~~~~~~~~~~~~~~~~~~~~~
描述：修改密码

地址：/api/user/sendPWResetMail/

HTTP请求方式：POST

参数：
	* email, 邮箱, 非空

返回数据：
::
	{
		status: 0 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		error: "Network Error!"
	}

===注册√√√
~~~~~~~~~~~~~
描述：注册

地址：/api/user/register/

HTTP请求方式：POST

参数：
	* username, 用户名, 非空
	* email, 密码, 非空
	* password1, 密码, 非空
	* password2, 密码确认, 非空

返回数据：
::
	{
		status: 0 (0 -- 请求失败, 返回error参数, 带上错误原因；1 -- 请求成功, 带上下述参数)
		token: 123fdesa324fea23
	}


个人主题模块
------------
===球场雷达√√√
~~~~~~~~~~~~~
描述：获取附近球场

地址：/api/court/getnearby/

HTTP请求方式：GET

参数：
	* page, 页码, 非空
	* size, 返回条数, 非空
	* latitude, 纬度, 非空
	* longitude, 经度, 非空

返回数据：
::
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		{
			id: 12 (球场ID)
			name: "北理工球场"
			photo: "http://XXX.com/field/12.jpg"  (图片URL)
			fee: "120 - 150" (费用)
			location: "中关村南大街5号院"
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		}
	}


球队雷达(该接口暂废弃)
~~~~~~~~~~~~~
描述：获取附近球队

地址：/api/team/getnearby/

HTTP请求方式：GET

参数：
	* page, 页码, 非空
	* size, 返回条数, 非空
	* latitude, 纬度, 非空
	* longitude, 经度, 非空 

返回数据：
::
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		{
			id: 12 (球队ID)
			name: "北理工球队"
			photo: "http://XXX.com/team/12.jpg"  (图片URL)
			admin: "PubGeek" (创建人)
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		}
	}

===球员雷达√√√
~~~~~~~~~~~~~
描述：获取附近球员

地址：/api/user/getnearby/

HTTP请求方式：GET

参数：
	* page, 页码, 非空
	* size, 返回条数, 非空
	* latitude, 纬度, 非空
	* longitude, 经度, 非空 

返回数据：
::
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		{
			id: 12 (球员ID)
			name: "世界波"
			avatar: "http://XXX.com/field/12.jpg"  (图片URL)
			height: "183" (身高)
			weight: "65" (体重)
			position: "前锋" (球队角色) 
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		}
	}



===搜索（球场、球队、球员）√√√

描述：搜索球场、球队、球员（返回搜索结果的前20条）**暂未限制数量**

地址：/api/radar/search/

HTTP请求方式：GET

参数：
	* keyword, 关键字, 非空
	* type, 雷达类型（0 -- 球场雷达, 1 -- 球队雷达, 2 -- 球员雷达）, 非空
	* latitude, 纬度, 非空
	* longitude, 经度, 非空

返回数据：
::
	type为0时
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		[{
			id: 12 (球场ID)
			name: "北理工球场"
			photo: "http://XXX.com/field/12.jpg"  (图片URL)
			fee: "120 - 150" (费用)
			location: "中关村南大街5号院"
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		} ...]
	}

	type为1时
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		[{
			id: 12 (球队ID)
			name: "北理工球队"
			photo: "http://XXX.com/team/12.jpg"  (图片URL)
			admin: "PubGeek" (创建人)
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		} ...]
	}
	
	type为2时
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		[{
			id: 12 (球员ID)
			name: "世界波"
			avatar: "http://XXX.com/field/12.jpg"  (图片URL)
			height: "183" (身高)
			weight: "65" (体重)
			position: "前锋" (球队角色) 
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		} ...]
	}


===详情（球场、球队、球员）√√√
~~~~~~~~~~~~~
描述：（球场、球队、球员）详情

地址：/api/radar/detail/

HTTP请求方式：GET

参数：
	* id, （球场、球队、球员）ID, 非空
	* type, 雷达类型（0 -- 球场雷达, 1 -- 球队雷达, 2 -- 球员雷达）, 非空
	* latitude, 纬度, 非空
	* longitude, 经度, 非空

返回数据：
::
	type为0时
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		{
			name: "世界波"
			photo: "http://XXX.com/field/12.jpg"  (图片URL)
			phone: 15212342342
			location: "中关村南大街5号院"
			fee: "120 - 150" (费用)
			eleven: 0
			nine: 1
			seven: 1
			five: 0
			parkingfee: "120 - 150" (停车费用)
			opentime: "9:00 - 16:00"（营业时间）
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		}
	}

	type为1时
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		{
			fullname: "北京理工大学校队"
			shortname: "北理工球队"
			founddate: 12134432432
			introduction: "大运会代表队"
			homeid:
			homename: 
			members:
			owner:
			sponsor:
			admin:
			captainid:
			captainname:
			scores:
			opponents:
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		}
	}
	
	type为2时
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		data: 
		[{
			name: "世界波"
			avatar: "http://XXX.com/field/12.jpg"  (图片URL)
			birthday: 123213213
			height: "183" (身高)
			weight: "65" (体重)
			position: "前锋" (球队角色) 
			location: 
			scores: 12
			level:
			latitude: 123.1234 (纬度)
			longitude: 123.1234 (经度)
			distance: 12.3 (单位：km)
		} ...]
	}

添加比赛记录
~~~~~~~~~~~~
描述: 添加比赛记录
地址: /api/team/addrecord/
HTTP请求方式: POST
参数:
    * selfteam 添加用户自己所在球队
    * opponent  对方球队
    * nature  比赛性质,可空
    * time 比赛时间 格式: 2002-02-02
    * place 场地 (使用外键或者字符串待定)
    * selfgoals 本队进球数
    * opgoals 对方进球数
    * users  [uid, goals, assist],...
返回数据:
::
	{
		status: 1 (0 -- 请求失败, 返回error参数, 带上错误原因；1 -- 请求成功, 带上下述参数)
	}

添加技能点
~~~~~~~~~~~~~
描述: 添加技能点
地址: /api/user/addskill/
HTTP请求方式: POST
参数:
    * token
    * physical
    * passing
    * sense
    * shooting
    * tech
返回数据:
::
	{
		status: 1 (0 -- 请求失败, 返回error参数, 带上错误原因；1 -- 请求成功, 带上下述参数)
	}

获取球队队员信息
~~~~~~~~~~~~~
描述: 获取球队队员信息
地址: /api/team/members/
HTTP请求方式: GET
参数:
    * tid
返回数据:
::
	{
		status: 1,
            members: [{user1},{user2},{user3}]
        }

更新team头像
~~~~~~~~~~~~~~~~~~~~
描述：更新team头像

地址：/api/team/updateavatar/

HTTP请求方式：POST

参数：
	* avatar, 图片文件, 非空
	* token, 当前用户标识, 非空 
	* id 球队id

返回数据：
::
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		url: "http://img"
	}


更新team资料
~~~~~~~~~~~~~
描述：更新team资料

地址：/api/team/updateprofile/

HTTP请求方式：POST

参数：
	* id  球队id
	* fullname  全称
	* shortname   简称
	* introduction  简介
	* contact 联系人
	* phone  手机号
	* home  主场id
返回数据：
::
	{
		status: 0 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		error: "Network Error!"
	}



发送比赛请求
~~~~~~~~~~~~~~~~~
描述：(你那里设置只有管理员能点击)：

url:  api/team/vs/

POST:
    - sid 管理员所在球队id (整数)
    - tid 目标球队  (整数)
    - vs_time 比赛时间  格式：2013-01-01 13:30
    - court 比赛场地  (字符窜)
返回数据:
::
    {
        "status": 1
    }


GET:
    - token 管理员token

返回数据:
::
{
    "status": 1, 
    "data": [{  'vs_id': j.id,
                        'apply_team': j.team_host.fullname,
                        'apply_time': j.apply_time,
                        'avatar': j.team_host._avatar(),
                        'contact': j.team_host.contact,
                        'phone': j.team_host.phone,
                        'vs_time': j.vs_time.strftime('%Y-%m-%d %H:%M'),
                        'is_done': j.is_done
                    }, {}, {}
                    ]
}

删除比赛请求记录
~~~~~~~~~~~~~~~~

url:  api/team/handle/

POST:
    - vs_id  记录的id值，上面接口获得

返回：
::
{"status": 1}



团队主题模块
------------
获取联赛
~~~~~~~~~~~~~

报名联赛
~~~~~~~~~~~~~

预约场地
~~~~~~~~~~~~~

预约比赛
~~~~~~~~~~~~~


