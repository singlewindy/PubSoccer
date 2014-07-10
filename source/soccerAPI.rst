世界波API调用文档
===============

用户模块
--------

获取用户资料
~~~~~~~~~~~~~
描述：根据UID获取用户资料(只能获取自己的)

地址：/api/user/getuserprofile/

HTTP请求方式：GET

参数：
	* token，用户标识, 非空

返回数据：
::
	{
		status: 1 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功,返回下述参数)
		data: 
		{
		    uid: 123
		    basic:
		    {
		    	nickname: "pubgeek"(昵称)
		    	email: "admin@pubgeek.com"
		    	avatar: "http://www.pubgeek.com/avatar/123"
		    	tid: 12
		    	teamname: "北理工校队"（为Team表中的shortname）
		    	sex: 1 (0 -- 女性，1 -- 男性)
		    	height: 183 (身高)
		    	weight: 75 (体重，单位为公斤)
		    	birthday: 1234324241 (时间戳格式)
		    	age: 21 (根据当前时间戳和birthday的时间戳来算年龄)
		    	province: "北京"
		    	city: "北京"
		    }
		    competitions:
		    [{
		    	time: 1234324241 (比赛时间，时间戳格式)
		    	place: "北京市海淀区北京理工大学" (比赛地点)
		    } ...]
		    honors: ["XX比赛一等奖", "XX比赛二等奖", ...]
		    skill:
		    {
		    	level: 3 (用户现有等级)
		    	exp: 123 (用户经验)
		    	star: 2 (用户星级)
		    }
		}
	}

===更新用户资料√√(需增加position字段)
~~~~~~~~~~~~~
描述：更新用户资料

地址：/api/user/updateuserprofile/

HTTP请求方式：POST

参数：
	* nickname, 昵称, 非空
	* sex (0--女性，1--男性), 性别, 非空
	* birthday, 生日, 非空
	* height, 身高, 非空
	* weight, 体重, 非空
	* position, 场上位置, 非空, String类型
	* tid, 球队ID, 可为空
	* province, 省份, 可为空
	* city, 城市, 可为空
	* token, 当前用户标识, 非空 

返回数据：
::
	{
		status: 0 (0 -- 请求失败，返回error参数，带上错误原因；1 -- 请求成功)
		error: "Network Error!"
	}

===创建球队√√√
~~~~~~~~~~~~~
描述：创建球队

地址：/api/user/createTeam/

HTTP请求方式：POST

参数：
	* fullname, 球队全称, 非空
	* shortname, 球队简称, 非空
	* introduction, 简介, 非空
	* fid, 球场ID, 非空
	* members, 球员数目, 非空
	* owner, 拥有者, 非空
	* sponsor, 赞助商, 非空
	* captain, 队长, 非空
	* location, 球队地点, 非空
	* latitude, 球队地点经度, 非空
	* longitude, 球队地点纬度, 非空
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


===球队雷达√√(待创建球队完成后测试)
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
~~~~~~~~~~~~~
描述：搜索球场、球队、球员（返回搜索结果的前20条）

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
			home: 
			members:
			owner:
			sponsor:
			admin:
			captain:
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


