---
title: json
date: 2021-10-11 19:02:23
tags: 编程
categories:
- [Java]
---

### 示例代码
* 获取json串中的key、value：
```
public static void testReadJson() {
        try
        {
            String heartbeatString = FileUtil.readJsonFile(
                    "/Users/liquangang/work/chengfeng2.0/baidu/face-link/face-link-deviceSimulation/src/test/java/com/baidu/facelink/websocket/testJson/Heartbeat.json");
            JsonParser p = new JsonParser();
            JsonElement e = p.parse(heartbeatString);
            jsonTree(e, new JsonKeyAndValueHandle() {
                @Override
                public void handleKey(String key) {
                    System.out.println(key);
                }

                @Override
                public void handleValue(JsonElement e) {
                    System.out.println(e.toString());
                }

                @Override
                public void handleKeyAndValue(Map.Entry<String, JsonElement> en) {
                    if (en.getKey().equals("deviceId")) {
                        en.setValue(new Gson().toJsonTree("DMCM020AYC21E00252"));
                    }

                    if (en.getKey().equals("appId")) {
                        en.setValue(new Gson().toJsonTree("692805283478"));
                    }
                }
            });

        }
        catch(Exception e)
        {
            e.printStackTrace();
        }
    }

    public static void jsonTree(JsonElement e, JsonKeyAndValueHandle jsonKeyAndValueHandle)
    {
        if (e.isJsonNull())
        {
            jsonKeyAndValueHandle.handleValue(e);
            return;
        }

        if (e.isJsonPrimitive())
        {
            jsonKeyAndValueHandle.handleValue(e);
            return;
        }

        if (e.isJsonArray())
        {
            JsonArray ja = e.getAsJsonArray();
            if (null != ja)
            {
                for (JsonElement ae : ja)
                {
                    jsonTree(ae, jsonKeyAndValueHandle);
                }
            }
            return;
        }

        if (e.isJsonObject())
        {
            Set<Map.Entry<String, JsonElement>> es = e.getAsJsonObject().entrySet();
            for (Map.Entry<String, JsonElement> en : es)
            {
                jsonKeyAndValueHandle.handleKey(en.getKey());
                jsonKeyAndValueHandle.handleKeyAndValue(en);
                jsonTree(en.getValue(), jsonKeyAndValueHandle);
            }
        }
    }

    public interface JsonKeyAndValueHandle {
        void handleKey(String key);
        void handleValue(JsonElement e);
        void handleKeyAndValue(Map.Entry<String, JsonElement> en);
    }

```