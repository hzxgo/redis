# redis
redis orm by golang
目前对redis的方法支持不全，需要的时候后期再添加

# 使用介绍--初始化单个实例

```
package main

import (
	"github.com/hzxgo/log"
	"github.com/hzxgo/redis"
)

func main() {
	address := "127.0.0.1:6379"
	db := 1
	timeout := 3
	auth := "redis_auth_string"
	// instance := "main"

	// init redis
	// 指定实例名称初始化：redis.Init(address, db, timeout, auth, instance)
	err := redis.Init(address, db, timeout, auth)
	if err != nil {
		log.Errorf("redis init | %v", err)
		return
	}

	// redis set
	// 指定实例：redis.Set(rdsUsername, "hezhixiong", instance)
	rdsUsername := "test:username"
	err = redis.Set(rdsUsername, "hezhixiong")
	if  err != nil {
		log.Errorf("redis set %s | %v", rdsUsername, err)
		return
	}

	// redis get
	username, err := redis.Get(rdsUsername)
	if err != nil {
		log.Errorf("redis get %s | %v", rdsUsername, err)
		return
	}

	log.Infof("username: %s", username)
}
```

# 初始化多个实例

```
rc := make([]*redis.RdsCfg, len(Config.Redis))
	for i, v := range Config.Redis {
		rc[i] = &redis.RdsCfg{
			Instance:  v.Instance,
			Address:   v.Address,
			DB:        v.Db,
			Auth:      v.Auth,
			Timeout:   v.Timeout,
			IsDefault: v.IsDefault,
		}
	}
	if err := redis.BatchInit(rc); err != nil {
		log.Errorf("batch init redis | %v", err)
		return
	}
```