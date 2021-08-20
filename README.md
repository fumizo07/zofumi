## filtrite(Bromite用広告ブロックフィルタ生成ツール)
filtriteは、次のフィルターリストを生成するためのプロジェクトです。 [Bromite](https://www.bromite.org/).
についてのページを参照してください。 詳細についてはこちらをご覧ください。[Custom Ad Block Filters](https://www.bromite.org/custom-filters) 

# Lists(リスト)
以下から任意のリストを選択し、リンクをコピーしてBromiteに追加できます。 設定に移動して、AdBlock settingsを選択。次に、フィルターURLをコピーしたものに設定します。

リストは次のとおりです。


| Link | Description  |
| ------ | ------|
| [Bromite Default](https://github.com/xarantolus/filtrite/releases/latest/download/bromite-default.dat) | Bromite [default filter list](https://github.com/bromite/filters), but generated by this tool |
| [Bromite Extended](https://github.com/xarantolus/filtrite/releases/latest/download/bromite-extended.dat) | The default list with additional annoyance blockers I use with [uBlock Origin](https://github.com/gorhill/uBlock) on Desktop |
| [German](https://github.com/xarantolus/filtrite/releases/latest/download/german.dat) | The "Bromite Extended" list with additional region-specific blocklists for german sites |

These lists are regularly updated automatically using GitHub Actions.

**Note**: I'm not 100% sure if all list formats that are used are actually supported by [the ruleset generation tool](https://github.com/xarantolus/subresource_filter_tools) (as the output indicates some failures). If you have a comment on that, please open an issue :)

### Using your own filter lists
This program is designed in a way that allows easily adding new lists. 

To create a new list:

1. このリポジトリをフォークしてください
2. lists→add file→Create new fileを選択して、ファイル名を入力してください。たぶんアルファベット小文字で最後が.txtじゃないとダメです。(例:adblockfilter.txt)
次に使用したいフィルタのURLをコピペしてCommit new fileをタップしてください。
Enable GitHub Actions by switching to the "Actions" tab of your repo, then confirming that you want to enable them
3. Choose a name for the list, e.g. `example-list`
4. Search for filter lists you want to use. You can for example find them [here](https://filterlists.com/), use those in "uBlock Origin" or "AdBlock Plus" format (however, it's possible that [not all types of rules are supported](https://github.com/bromite/bromite/wiki/AdBlocking)). Go to info, then "View" and copy the URL to the list.
5. Create a file `lists/example-list.txt` (aka in the `lists` directory) that contains the URLs to filter lists you copied before. It should look like this:
    ```
    # Lines starting with # are comments, empty lines are also allowed
    # List one URL per line:
    https://easylist.to/easylist/easylist.txt
    https://...

    # The following line doesn't work, only put either a comment or an URL in one line, not both
    http://  # Invalid comment on URL
    ```
5. Save your file, commit and push. GitHub actions should now build the list and create a release
6. After GitHub Actions generated the release, you can copy the linked URL in the release to always get the latest generated version. This URL looks something like `https://github.com/USERNAME/filtrite/releases/latest/download/FILENAME.dat`. 
7. Check that the generated filter file size is less than the allowed maximum of [10 MB](https://github.com/bromite/bromite/blob/e5771ef891cf01dd5aeaaec5e092841929a9a541/build/patches/Bromite-AdBlockUpdaterService.patch#L1152-L1153). If it isn't, you must remove some lists
8. Set this URL as the filter file in Bromite settings.

### [License](LICENSE)
This is free as in freedom software. Do whatever you like with it.
