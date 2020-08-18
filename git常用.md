git常用：http://www.blognet.cn/?p=880

git stash 將修改暫未提交的部分暂存缓冲区

```go
//商品上架下架处理
    backendShopUpAndDown(r)

    accesstoken(r)
}

//商品上架下架配置
func backendShopUpAndDown(r gin.IRoutes) {
    r.POST("/backend/shop-config/up-and-down/", func(c *gin.Context) {
        type Param struct {
            GameId       int `json:"game_id" binding:"required"`
            ShopConfigId int `json:"shop_config_id" binding:"required"`
            Status       int `json:"status" binding:"required"`
        }
        var param Param
        if e := c.Bind(&param); e != nil {
            c.JSON(400, gin.H{"message": errorx.Wrap(e).Error()})
            return
        }

        conn := redistool.RedisPool.Get()
        defer conn.Close()

        sip := shopModel.ShopConfig{
            GameId: param.GameId,
            Id:     param.ShopConfigId,
        }
        engine := db.DB.Model(&shopModel.ShopConfig{}).Where("game_id=? id=?", param.GameId, param.ShopConfigId)

        if e := sip.MustGet(conn, engine); e != nil {
            if e != redis.ErrNil && e.Error() != "not found record in db nor redis" {
                common.SaveError(errorx.Wrap(e), map[string]interface{}{
                    "param": param,
                })
                c.JSON(200, gin.H{
                    "message": "success",
                    "tip":     "获取道具记录失败，稍后重试",
                    "tip_id":  1, "debug_message": errorx.Wrap(e).Error(),
                })
                return
            }
            c.JSON(200, gin.H{
                "message": "success",
                "tip":     "暂无记录",
                "tip_id":  2,
            })
            return
        }
        if sip.Status == param.Status {
            c.JSON(200, gin.H{
                "message": "success",
                "tip":     "请勿重复操作",
                "tip_id":  1,
            })
            return
        }
        sql := "update shop_config set status=? where id=?"
        if ret := db.DB.Raw(sql, param.Status, param.ShopConfigId); ret != nil {
            c.JSON(200, gin.H{
                "message": "success",
                "tip":     "修改失败",
            })
            return
        }
        sip.DeleteFromRedis(conn)
        return
    })
}

```

git 回退版本：

git log查看历史版本

git reset --hard 版本号

git push -f -u origin 分支名

常用git stash命令：

（1）**git stash** save "save message" : 执行存储时，添加备注，方便查找，只有git stash 也要可以的，但查找时不方便识别。

（2）**git stash list** ：查看stash了哪些存储

（3）**git stash show** ：显示做了哪些改动，默认show第一个存储,如果要显示其他存贮，后面加stash@{$num}，比如第二个 git stash show stash@{1}

（4）**git stash show -p** : 显示第一个存储的改动，如果想显示其他存存储，命令：git stash show stash@{$num} -p ，比如第二个：git stash show stash@{1} -p

（5）**git stash apply** :应用某个存储,但不会把存储从存储列表中删除，默认使用第一个存储,即stash@{0}，如果要使用其他个，git stash apply stash@{$num} ， 比如第二个：git stash apply stash@{1} 

（6）**git stash pop** ：命令恢复之前缓存的工作目录，将缓存堆栈中的对应stash删除，并将对应修改应用到当前的工作目录下,默认为第一个stash,即stash@{0}，如果要应用并删除其他stash，命令：git stash pop stash@{$num} ，比如应用并删除第二个：git stash pop stash@{1}

（7）**git stash drop** stash@{$num} ：丢弃stash@{$num}存储，从列表中删除这个存储

（8）`**git stash clear** ：`删除所有缓存的stash