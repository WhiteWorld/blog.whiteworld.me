{
    "date": "2015-01-22",
    "description": null,
    "draft": false,
    "id": 12,
    "image": null,
    "meta_title": null,
    "slug": "tmux-cli-tutorial",
    "tags": [
        "Tutorial",
        "Cli",
        "Tmux"
    ],
    "title": "Tmux \u547d\u4ee4\u4f7f\u7528",
    "type": "post"
}


### session管理

- 新建一个session
	  
	  tmux new -s session_name

- attach一个session
      
      tmux attach -t session_name

- 切换session
	  
	  tmux switch -t session_name

- 列出存在的session
	  
	  tmux ls

- detach 当前session
	
	  tmux detach 或者 prefix + d

- 杀死session
	
	  tmux kill-session -t session_name

### 窗口管理

- 新建窗口
	  
	  tmux new-window 或者 prefix + c

- 切换窗口
	  
	  tmux select-window -t :0-9 或者 prefix + 0-9

- 重命名窗口
	  
	  tmux rename-window 或者 prefix + ,

### 面板管理

- 水平分割窗口
	  
	  tmux split-window -h 或者 prefix + %

- 竖直分割窗口
	 
	  tmux split-window 或者 prefix + "

- 交换面板
	  
	  prefix + { or }

- 切换面板
	  
	  prefix + [UDLR]

- 关闭面板
	  
	  prefix + x

### 其他

- 滚屏
	
	  prefix + [  退出 q

- 时钟
	  
	  prefix + t 退出 q