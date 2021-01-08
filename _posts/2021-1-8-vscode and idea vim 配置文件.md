<!--
 * @Author: your name
 * @Date: 2021-01-08 09:45:18
 * @LastEditTime: 2021-01-08 09:49:12
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \Ten000hours.github.io\_posts\2021-1-8-vscode and idea vim 配置文件.md
-->
# Config

## vscode 

'''c

    // 设置leader键为空格键
    "vim.leader": "<space>",
    "vim.insertModeKeyBindings": [
     {
         "before": ["j", "j"],
         "after": ["<esc>"]
     },

             {
            "before": [
                "<C-i>"
            ] ,
            "commands": [
              "cursorUp"
            ],
        },
             {
            "before": [
                "<C-k>"
            ] ,
            "commands": [
              "cursorDown"
            ],
        },       
             {
            "before": [
                "<C-j>"
            ] ,
            "commands": [
              "cursorLeft"
            ],
        },       
             {
            "before": [
                "<C-l>"
            ] ,
            "commands": [
              "cursorRight"
            ],
        },       




     


     


],
    "vim.normalModeKeyBindingsNonRecursive": [
//更改vim的键位，把h变成光标前输入，ijkl变成上、左、下、右，这样更符合人体习惯
//我只用了一回就熟练掌握了，而且再也不想回到hjkl表示上下左右的别扭方式了。
//   i               ↑
//j  k  l        ←  ↓  →
        {
            "before": [
                "h"
            ],
            "after": [
                "i"
            ]
        },

        
        {
            "before": [
                "h"
            ],
            "after": [
                "i"
            ]
        },
        {
            "before": [
                "j"
            ],
            "after": [
                "h"
            ]
        },
        {
            "before": [
                "k"
            ],
            "after": [
                "j"
            ]
        },
        {
            "before": [
                "i"
            ],
            "after": [
                "k"
            ]
        },
        {
            "before": [
                "H"
            ],
            "after": [
                "I"
            ]
        },
        {
            "before": [
                "J"
            ],
            "after": [
                "H"
            ]
        },
        {
            "before": [
                "K"
            ],
            "after": [
                "J"
            ]
        },
        {
            "before": [
                "I"
            ],
            "after": [
                "K"
            ]
        },
      
        // 按下leader键加r键，如果还未开始调试，则不进行调试，直接运行文件
        {
            "before": [
                "<leader>",
                "r",
            ],
            "commands": [
                "workbench.action.debug.run"
            ],
            "when": [
                "!inDebugMode"
            ],
        },
        {
            "before": [
                "<leader>",
                "j",
            ],
            "commands": [
                "workbench.action.navigateLeft",
            ]
        },
        {
            "before": [
                "<leader>",
                "l",
            ],
            "commands": [
                "workbench.action.navigateRight",
            ]
        },
 {
            "before": [
                "<leader>",
                "i",
            ],
            "commands": [
                "workbench.action.navigateUp",
            ]
        },
 {
            "before": [
                "<leader>",
                "k",
            ],
            "commands": [
                "workbench.action.navigateDown",
            ]
        },
        // 按下leader键加r键，如果正在调试时，则重新运行文件（restart）
        {
            "before": [
                "<leader>",
                "r",
            ],
            "commands": [
                "workbench.action.debug.restart"
            ],
            "when": [
                "inDebugMode"
            ],
        },
        // 按下leader键加d键，开始调试
        {
            "before": [
                "<leader>",
                "d",
            ],
            "commands": [
                "workbench.action.debug.start"
            ]
        },
        // 按下leader键+w，保存当前文件
        {
            "before": [
                "<leader>",
                "w",
            ],
            "commands": [
                "workbench.action.files.save",
            ],
        },
        // 按下leader键+b，新建文件（buffer缓冲区，暂时写点东西，将来不一定保存）
        {
            "before": [
                "<leader>",
                "b",
            ],
            "commands": [
                "workbench.action.files.newUntitledFile",
            ]
        },
        // 按下leader键+t+n，新建标签/文件并命名（命名后保存，这个是自己要用的文件，与上面的仅缓冲区不同）（tab new）
        // 因为文件以类似网页标签的形式排布，故使用tab的含义
        {
            "before": [
                "<leader>",
                "t",
                "n",
            ],
            "commands": [
                "workbench.action.files.newUntitledFile",
                "workbench.action.files.save",
            ]
        },
        // 按下leader键+t+o，关闭其他标签/文件（tab only）
        {
            "before": [
                "<leader>",
                "t",
                "o",
            ],
            "commands": [
                "workbench.action.closeOtherEditors",
            ]
        },
        // 按下leader键+q，退出，不保存当前文件
        {
            "before": [
                "<leader>",
                "q",
            ],
            "commands": [
                ":q!",
            ],
        },
        // 连着按下两个Z键，保存并关闭当前标签/文件
        {
            "before": [
                "Z",
                "Z",
            ],
            "commands": [
                "workbench.action.files.save",
                "workbench.action.closeActiveEditor"
            ],
        },


        // 按下leader键+k，向上搜索行（easymotion）
        {
            "before": [
                "<leader>",
                "k"
            ],
            "after": [
                "<leader>",
                "<leader>",
                "k",
            ]
        },
        // 按下leader键+j，向下搜索行（easymotion）
        // {
        //     "before": [
        //         "<leader>",
        //         "j"
        //     ],
        //     "after": [
        //         "<leader>",
        //         "<leader>", j
        //         "j",
        //     ]
        // },
        // // 按下leader键+s，搜索以两个字符开始的匹配（easymotion）
        {
            "before": [
                "<leader>",
                "s"
            ],
            "after": [
                "<leader>",
                "<leader>",
                "2",
                "s",
            ]
        },
        // 按下leader键+f，向后搜索以单个字符开始的匹配（easymotion）
        {
            "before": [
                "<leader>",
                "f"
            ],
            "after": [
                "<leader>",
                "<leader>",
                "f",
            ]
        },
        // 按下leader键+F，向前搜索以单个字符开始的匹配（easymotion）
        {
            "before": [
                "<leader>",
                "F"
            ],
            "after": [
                "<leader>",
                "<leader>",
                "F",
            ]
        },
    ],
    "vim.visualModeKeyBindingsNonRecursive": [
        //更改vim的键位，把h变成光标前输入，ijkl变成上、左、下、右，这样更符合人体习惯
        //我只用了一回就熟练掌握了，而且再也不想回到hjkl表示上下左右的别扭方式了。
        //   i               ↑
        //j  k  l        ←  ↓  →
        {
            "before": [
                "h"
            ],
            "after": [
                "i"
            ]
        },
        {
            "before": [
                "j"
            ],
            "after": [
                "h"
            ]
        },
        {
            "before": [
                "k"
            ],
            "after": [
                "j"
            ]
        },
        {
            "before": [
                "i"
            ],
            "after": [
                "k"
            ]
        },
        {
            "before": [
                "H"
            ],
            "after": [
                "I"
            ]
        },
        {
            "before": [
                "J"
            ],
            "after": [
                "H"
            ]
        },
        {
            "before": [
                "K"
            ],
            "after": [
                "J"
            ]
        },
        {
            "before": [
                "I"
            ],
            "after": [
                "K"
            ]
        },
    ],
    "vim.easymotion": true,
    "editor.fontLigatures": null,
}

'''


## idea 
