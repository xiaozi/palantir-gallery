# Palantir UI 界面目录

从 126 条公开视频里整理出的界面状态目录。每条记录是一种可区分的界面，附一张代表截图，以及回到原视频的时间点。

当前一共 **2737** 个界面状态，来自 **12865** 帧，归在 **205** 个应用下。

## 怎么看

在本目录启动一个静态服务器，然后打开画廊：

```bash
python3 -m http.server 8000
```

浏览器访问 <http://127.0.0.1:8000/gallery.html>。

画廊可以按产品、应用、可信度筛选，也可以搜索界面名、状态说明和画面文字。点开一张卡片可以看到完整截图、出现过的视频和时间点。左右方向键切换当前筛选结果里的上一条和下一条。卡片用 `screens/thumbs/` 里的缩略图，详情用 `screens/` 里的原图。

`catalog.md` 是同一份目录的 Markdown 版本，按产品和应用程序排列，每条带截图和视频链接。`catalog.json` 是对应的结构化数据。

## 目录里有什么

| 文件 | 内容 |
| --- | --- |
| `gallery.html` | 单页画廊。条目和 3 条文档替代说明直接写在页面里，打开即可筛选。 |
| `catalog.md` | 给人读的目录。 |
| `catalog.json` | 机器可读目录，含 `entries` 和未收入画廊的 `dropped`。 |
| `screens/` | 每个状态一张代表截图，`s001.jpg` … `s2737.jpg`。 |
| `screens/thumbs/` | 画廊卡片用的缩略图。 |

## 一条记录长什么样

`entries` 里每条大致如下：

```json
{
  "id": "s001",
  "product": "AIP",
  "app": "AI Hivemind",
  "screen": "Critique",
  "state": "Edit Criteria dialog (guidance, task, subtasks)",
  "confidence": "high",
  "evidence": "same app; speaker: criteria generated on the fly",
  "frames": 1,
  "key_text": ["Edit Criteria", "Guidance", "Task"],
  "candidates": ["c057"],
  "screenshot": "screens/s001.jpg",
  "docs": [],
  "occurrences": [
    {
      "video_id": "YLBnmtqeljw",
      "title": "Product Launch: Mindkit | DevCon 5",
      "upload_date": "20260309",
      "url": "https://www.youtube.com/watch?v=YLBnmtqeljw",
      "ranges": [
        { "start": 211.0, "end": 211.0, "link": "https://www.youtube.com/watch?v=YLBnmtqeljw&t=211s" }
      ]
    }
  ]
}
```

`confidence` 是应用名的把握：`high` / `medium` / `low`。为「中」或「低」时，应用名是根据画面和旁白推断的。`frames` 是归到这个状态的帧数。`key_text` 是画面上读到的文字。`docs` 是相关文档的相对路径。`occurrences` 记录它出现在哪些视频的哪些时间段。

画廊里的文档链接指向本仓库上一级的 `docs/`。单独克隆本仓库时，这些链接没有对应文件。页面另外带有 3 条文档状态说明（Legacy 或将被替代），可用「只看文档已标明替代」筛出来。这 3 条写在 `gallery.html` 里，不在 `catalog.json` 里。

## 规模

| 产品 | 界面状态 |
| --- | ---: |
| Foundry | 2292 |
| AIP | 281 |
| External | 142 |
| Gotham | 9 |
| security | 5 |
| Apollo | 4 |
| functions | 4 |

可信度：高 2345，中 367，低 25。2252 条挂了文档路径，涉及 84 篇文档。126 条视频里共 2873 次出现、4042 个时间段。

`catalog.json` 的 `dropped` 有 370 条候选，没有放进目录。常见原因是加载画面、片头片尾、舞台镜头、空白帧，或聚类过粗后已拆开重分。每条只有候选编号、原因，以及源素材里的代表帧路径；那些帧不在本仓库里。

## 许可

[MIT](LICENSE)
