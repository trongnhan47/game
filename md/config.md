# DUCK HUB - GROW A GARDEN 2

================================================================================
          DUCK HUB - GROW A GARDEN 2 - HƯỚNG DẪN CẤU HÌNH CHI TIẾT USERCONFIG
================================================================================

Tài liệu này hướng dẫn chi tiết cách thiết lập bảng cấu hình `getgenv().UserConfig` 
trong file `config.lua` cho bản Kaitun Grow A Garden 2.

--------------------------------------------------------------------------------
I. CẤU HÌNH HỆ THỐNG & HIỆU NĂNG
--------------------------------------------------------------------------------
1. ["FPS Cap"] (Số nguyên)
   - Ý nghĩa: Giới hạn số khung hình trên giây (FPS) của game.
   - Cách tùy biến: Đặt từ 1 đến 60. Mức khuyên dùng khi treo nhiều acc là 5 - 10.
   - Cách tắt: Đặt bằng nil hoặc xóa dòng này.
   - Ví dụ:
     ["FPS Cap"] = 7, -- Giới hạn 7 FPS để siêu nhẹ máy

--------------------------------------------------------------------------------
II. CẤU HÌNH TRỒNG TRỌT & THU HOẠCH (SEEDS / GARDEN)
--------------------------------------------------------------------------------
1. ["Auto Buy Seed"] (boolean)
   - Ý nghĩa: Tự động mua hạt giống trong Seed Shop khi cửa hàng restock.
   - Cách tùy biến: `true` (mở), `false` (tắt).
   - Khi tắt: Sẽ không mua thêm hạt giống từ shop tự động.

2. ["Auto Plant Seed"] (boolean)
   - Ý nghĩa: Bật/tắt toàn bộ tiến trình gieo hạt của bot.
   - Cách tùy biến: `true` (mở), `false` (tắt hoàn toàn việc gieo hạt).

3. ["Auto Plant"] (boolean)
   - Ý nghĩa: Chọn chế độ gieo hạt thông minh (Auto) hoặc thủ công (Limit).
     + true: Chế độ thông minh. Bot tự gieo các hạt có độ hiếm cao nhất/xịn nhất trong kho.
             Nếu đất đầy (đạt giới hạn Limit Auto Plant), bot sẽ tự đào các cây thường/yếu 
             để nhường chỗ gieo các hạt hiếm hơn.
     + false: Chế độ thủ công. Bot chỉ trồng các hạt được chỉ định số lượng trong "Limit Plant Seed".
   - Cách tùy biến: `true` hoặc `false`.

4. ["Limit Auto Plant"] (Số nguyên)
   - Ý nghĩa: Giới hạn tổng số lượng cây tối đa được trồng trên mảnh đất khi ["Auto Plant"] = true.
   - Cách tùy biến: Đặt con số bằng hoặc nhỏ hơn tổng số ô đất hiện có (Ví dụ: 800).

5. ["Blacklist Seed"] (Table danh sách)
   - Ý nghĩa: Danh sách hạt giống CẤM gieo. Bot sẽ không bao giờ tự trồng các loại hạt này.
   - Cách tùy biến: Khai báo danh sách chuỗi tên hạt giống.
   - Cách tắt: Để bảng rỗng `{}`.
   - Ví dụ:
     ["Blacklist Seed"] = {"Carrot", "Strawberry"}, -- Cấm trồng Carrot và Strawberry

6. ["Limit Plant Seed"] (Table Key-Value)
   - Ý nghĩa: Quy định số cây trồng tối đa cho từng loại cụ thể (chỉ có tác dụng khi ["Auto Plant"] = false).
   - Định dạng: `["Tên hạt giống"] = Số lượng cây`
   - Cách tắt: Để bảng rỗng `{}` hoặc xóa các dòng trong đó.
   - Ví dụ:
     ["Limit Plant Seed"] = {
         ["Carrot"] = 50, -- Chỉ trồng tối đa 50 cây Carrot cùng một lúc
     }

7. ["Limit Buy Seed"] (Table Key-Value)
   - Ý nghĩa: Giới hạn số lượng hạt trữ trong túi đồ. Bot sẽ mua tích lũy cho đến khi đạt số này.
   - Định dạng: `["Tên hạt giống"] = Số lượng trữ tối đa`
   - Ví dụ:
     ["Limit Buy Seed"] = {
         ["Tulip"] = 300, -- Trữ tối đa 300 hạt Tulip, đủ thì không mua thêm
     }

8. ["Harvest Mutation Only"] (Table nâng cao)
   - Ý nghĩa: Chỉ thu hoạch những loại cây đạt đột biến (Mutation) mong muốn, cây thường/cây không đột biến sẽ giữ lại không thu hoạch.
   - Cách hoạt động cực kỳ linh hoạt:
     + Nếu để trống `{}` hoặc không cài: Tất cả cây đều thu hoạch bình thường (cả cây thường lẫn đột biến).
     + Nếu thêm tên cây dạng chuỗi (Ví dụ: `"Bamboo"`): Chỉ thu hoạch Bamboo khi nó có BẤT KỲ đột biến nào (không thu hoạch Bamboo thường).
     + Nếu định nghĩa dạng bảng (Ví dụ: `["Tomato"] = {"Rainbow", "Gold"}`): Chỉ thu hoạch Tomato khi có đột biến cụ thể là Rainbow hoặc Gold.
     + Lưu ý: Các cây KHÔNG có tên trong danh sách này sẽ luôn được thu hoạch bình thường.
   - Ví dụ:
     ["Harvest Mutation Only"] = {
         "Bamboo", -- Chỉ thu hoạch Bamboo đột biến (bất kỳ loại đột biến nào)
         ["Tomato"] = {"Rainbow", "Gold", "Electric"}, -- Chỉ thu hoạch Tomato nếu đột biến là Rainbow, Gold, hoặc Electric.
         "Apple", -- Chỉ thu hoạch Apple đột biến
     }

9. ["Blacklist Shovel"] (Table danh sách)
   - Ý nghĩa: Danh sách các cây/đột biến CẤM dùng xẻng đào đi (bảo vệ cây hiếm khỏi bị đào mất khi dọn đất).
   - Định dạng: Chứa danh sách chuỗi tên hạt hoặc loại đột biến.
   - Ví dụ:
     ["Blacklist Shovel"] = {"Rainbow", "Gold", "Venom Spitter"} -- Cấm đào mọi cây có đột biến Rainbow, Gold hoặc cây Venom Spitter.

10. ["Shovel Plant Once"] (Table danh sách)
    - Ý nghĩa: Dùng xẻng đào sạch các cây trong danh sách này NGAY KHI SCRIPT VỪA KHỞI ĐỘNG (chỉ chạy 1 lần duy nhất). Cực kỳ hữu dụng để dọn sạch các cây rác/cây thường còn sót từ phiên chạy trước để lấy chỗ trống.
    - Cách hoạt động: Kiểm tra toàn bộ mảnh đất, nếu thấy cây có tên trùng với danh sách này (và không bị cấm bởi Blacklist Shovel) thì sẽ tự động đào đi.
    - Cách tắt: Để bảng rỗng `{}`.
    - Ví dụ:
      ["Shovel Plant Once"] = {"Carrot", "Tomato"} -- Khi bật script lên, tự đào sạch Carrot và Tomato thường trên đất.

11. ["Favorite"] (Table Key-Value)
    - Ý nghĩa: Tự động khóa (Favorite) các loại quả sau khi thu hoạch nếu đạt đột biến mong muốn, bảo vệ quả xịn không bị bán/gửi mail nhầm.
    - Ví dụ:
      ["Favorite"] = {
          ["Tomato"] = {"Rainbow", "Gold"}, -- Tự khóa Tomato nếu đột biến là Rainbow hoặc Gold.
      }

--------------------------------------------------------------------------------
III. CẤU HÌNH THÚ CƯNG (PETS)
--------------------------------------------------------------------------------
1. ["Buy Pets"] (Table Key-Value)
   - Ý nghĩa: Tự động mua thú cưng hoang dã xuất hiện trên bản đồ khi đủ tiền (Sheckles).
   - Cách hoạt động:
     + Nếu cài số: `["Frog"] = 999` -> Mua Frog cho tới khi tổng số Frog đạt 999 con.
     + Nếu cài bảng chi tiết: `["Deer"] = {Normal = 6, Huge = 99, Rainbow = 99}`
       -> Giới hạn tổng số lượng mua bằng tổng các số (6 + 99 + 99 = 204).
       -> Kiểm tra điều kiện riêng của từng loại hoang dã xuất hiện: nếu là Deer thường thì chỉ mua khi số Deer thường sở hữu < 6; nếu là Deer Huge thì mua khi số Deer Huge sở hữu < 99.
   - Cách tắt: Đặt bằng 0, xóa tên pet hoặc để bảng rỗng `{}`.

2. ["Equip Pets"] (Table danh sách các Table con)
   - Ý nghĩa: Tự động trang bị thú cưng theo độ ưu tiên và bộ lọc thuộc tính.
   - Định dạng: `{ "Tên Pet", Giới hạn số lượng đeo, Độ ưu tiên (số nhỏ đeo trước), Bộ lọc }`
   - Bộ lọc (tham số thứ 4) có thể là:
     + Một chuỗi: `"Normal"`, `"Huge"`, `"Rainbow"`, `"Big"`.
     + Một table danh sách: `{"Huge", "Rainbow"}`.
     + Nếu bỏ trống bộ lọc: Bot tự đeo theo thứ tự từ mạnh đến yếu (Huge > Big > Rainbow > Normal).
   - Ví dụ:
     ["Equip Pets"] = {
         {"Deer", 1, 1, "Normal"},             -- Đeo tối đa 1 con Deer loại thường (Ưu tiên số 1)
         {"Robin", 6, 2, {"Huge", "Rainbow"}}, -- Đeo tối đa 6 con Robin nếu là Huge hoặc Rainbow (Ưu tiên số 2)
         {"Bunny", 6, 3, "Normal"},            -- Đeo Bunny thường (Ưu tiên số 3)
         {"Frog", 6, 4},                       -- Đeo Frog tự động tối ưu (Ưu tiên số 4)
     }
   - Cách tắt: Để bảng rỗng `{}`.

3. ["Unlock Pet Slots"] (Số nguyên)
   - Ý nghĩa: Tự động mua thêm ô trang bị thú cưng (Pet Slot) bằng tiền game cho đến khi đạt giới hạn này.
   - Cách tắt: Đặt bằng `nil` hoặc `false` hoặc `0`.

--------------------------------------------------------------------------------
IV. CẤU HÌNH MỞ RỘNG ĐẤT (PLOT EXPANSION)
--------------------------------------------------------------------------------
1. ["Expand Plot"] (boolean)
   - Ý nghĩa: Tự động mua mở rộng diện tích đất trồng (Plot) khi đủ tiền.
   - Cách tắt: Đặt `false`.

2. ["Plot Expansions"] (Số nguyên)
   - Ý nghĩa: Giới hạn cấp độ mở rộng tối đa (Ví dụ: 3 thì chỉ mở rộng đến cấp 3 sẽ dừng).
   - Cách tắt: Đặt `0` hoặc tắt bằng cách cài ["Expand Plot"] = false.

--------------------------------------------------------------------------------
V. CẤU HÌNH TRANG BỊ & DỤNG CỤ (GEARS)
--------------------------------------------------------------------------------
1. ["Gears"] (Table phức hợp)
   - Gồm hai mục con:
     + ["Buy Gear"] (Table Key-Value hoặc Danh sách): Tự động mua dụng cụ làm vườn từ shop.
       * Định dạng 1 (Dạng mảng): `"Uncommon Sprinkler"` -> Mặc định mua tối đa giới hạn là 50 cái.
       * Định dạng 2 (Key-Value): `["Common Watering Can"] = 9999` -> Mua tối đa 9999 cái.
     + ["Gears To Use"] (Table danh sách): Danh sách dụng cụ được phép sử dụng.
       * Bot sẽ quét túi đồ của bạn, lọc ra những món có tên trong danh sách này và tự chọn món có GIÁ MUA CAO NHẤT (xịn nhất) để đem ra tưới nước/đặt vòi phun.
   - Cách tắt: Để các bảng trong đó rỗng `{}`.

--------------------------------------------------------------------------------
VI. CẤU HÌNH WEBHOOK (THÔNG BÁO DISCORD)
--------------------------------------------------------------------------------
1. ["Webhook Pet URL"], ["Webhook Seed URL"], ["Webhook Gear URL"] (Chuỗi URL)
   - Ý nghĩa: Các đường dẫn Webhook gửi thông báo Discord riêng biệt cho Pet, Hạt giống, và Trang bị.
   - Cách tắt: Để trống `""`, đặt bằng `nil` hoặc `false`.

2. ["Webhook Pet Name"] (Table danh sách)
   - Ý nghĩa: Danh sách tên thú cưng muốn thông báo.
   - Nếu để trống `{}` hoặc không khai báo: Sẽ mặc định thông báo cho TẤT CẢ các loại pet nhận được.

3. ["Webhook Pet Rarity"] (Table danh sách)
   - Ý nghĩa: Danh sách độ hiếm thú cưng muốn thông báo (Ví dụ: `{"Mythic", "Super", "Secret"}`).

4. ["Webhook Pet Type"] / ["Webhook Pet Size"] (Table danh sách)
   - Ý nghĩa: Lọc loại pet (như Rainbow) hoặc kích thước pet (như Huge) để gửi thông báo.

5. ["Webhook Odds"] (Số hoặc Chuỗi viết tắt)
   - Ý nghĩa: Chỉ thông báo pet có tỷ lệ nở/tame cực hiếm lớn hơn hoặc bằng mức này.
   - Ví dụ: `1000` hoặc `"1k"`, `"1.5m"`, `"2b"`.

6. ["Webhook Seed Name"] (Table danh sách)
   - Ý nghĩa: Chỉ gửi thông báo Discord khi nhận được hạt giống nằm trong danh sách này (Bắt buộc phải khai báo tên, nếu để trống sẽ không gửi thông báo hạt giống).
   - Ví dụ: `{"Rainbow", "Gold", "Moon Bloom"}`

7. ["Webhook Gear Name"] (Table danh sách)
   - Ý nghĩa: Chỉ gửi thông báo Discord khi mua thành công trang bị nằm trong danh sách này (Bắt buộc khai báo tên).
   - Ví dụ: `{"Super Sprinkler", "Super Watering Can"}`

8. ["Webhook Note"] (Chuỗi)
   - Ý nghĩa: Ghi chú tùy chỉnh hiển thị trong tin nhắn Webhook (Ví dụ: tên máy treo, tên acc).

9. ["Discord ID"] (Chuỗi số)
   - Ý nghĩa: Điền ID tài khoản Discord của bạn (Ví dụ: `"229850538911596545"`). Bot sẽ tự động PING thẻ bạn trên Discord khi nhận được Pet hoặc Hạt cực hiếm.

--------------------------------------------------------------------------------
VII. CẤU HÌNH TỰ ĐỘNG GỬI THƯ (MAILBOX SYSTEM)
--------------------------------------------------------------------------------
1. ["Mail To Username"] (Bảng danh sách hoặc Chuỗi)
   - Ý nghĩa: Danh sách các tên người nhận mặc định.
   - Cách hoạt động: Nếu một vật phẩm cần gửi mail không được cài đặt người nhận cụ thể (To), bot sẽ chọn ngẫu nhiên một tên trong danh sách này để gửi tới.
   - Ví dụ: `{"dannyhuynh"}` hoặc `{"acc_phu1", "acc_phu2"}`.

2. ["Mail Cooldown Secs"] (Số nguyên)
   - Ý nghĩa: Thời gian chờ tối thiểu giữa các lần gửi mail (giây). Mặc định là 60 giây nếu không cài.

3. ["Claim Mail"] (boolean)
   - Ý nghĩa: Tự động mở hòm thư để nhận quà tặng (Gifts) và đồng ý lời mời bang hội (Guild Invites) mỗi 30 giây.
   - Cách tắt: Đặt `false`.

4. ["Items To Mail"] (Table phức hợp gồm Pet, Seed, Gear)
   - Ý nghĩa: Tự động đóng gói và gửi vật phẩm qua Mailbox khi đạt đủ số lượng trong kho đồ.
   - Cách cấu hình từng nhóm:
     + **Nhóm ["Pet"]**:
       * Cấu hình số lượng: `["Monkey"] = 5` -> Khi có từ 5 con Monkey trở lên (không phân biệt size/hệ), tự gửi mail tất cả Monkey cho tài khoản mặc định.
       * Cấu hình chi tiết (To & Size):
         `["Unicorn"] = {Huge = 9, Rainbow = 9, To = "kelvincat"}` -> Chỉ gửi Unicorn loại Huge (khi số Huge >= 9) hoặc hệ Rainbow (khi số Rainbow >= 9) cho tài khoản "kelvincat". Các loại Unicorn thường khác sẽ giữ lại không gửi.
         `["Golden Dragonfly"] = {All = 10, To = "tomtunglan"}` -> Khi tổng số lượng Golden Dragonfly các loại đạt >= 10 con, gửi toàn bộ qua "tomtunglan".
     + **Nhóm ["Seed"]**:
       * Cấu hình số lượng: `["Gold"] = 20` -> Khi có >= 20 hạt Gold, gửi cho tài khoản mặc định.
       * Cấu hình chi tiết: `["Rainbow"] = {Amount = 1, To = "htstock"}` -> Có từ >= 1 hạt Rainbow sẽ gửi ngay cho "htstock".
     + **Nhóm ["Gear"]**:
       * Cấu hình số lượng: `["Super Sprinkler"] = 1` -> Khi có >= 1 cái Super Sprinkler trong túi, gửi cho tài khoản mặc định.
       * Cấu hình chi tiết: `["Super Watering Can"] = {Amount = 1, To = "tungsahur"}` -> Có >= 1 cái sẽ gửi qua "tungsahur".
   - Cách tắt gửi mail: Đặt bảng `Items To Mail` rỗng hoặc đặt `Items To Mail = nil/false`.

--------------------------------------------------------------------------------
VIII. NGUYÊN TẮC HOẠT ĐỘNG KHI ĐỂ TRỐNG (DEFAULT / EMPTY VALUES)
--------------------------------------------------------------------------------
1. Các giá trị boolean (true/false): Nếu không khai báo, script sẽ tự nhận giá trị mặc định được định nghĩa sẵn trong mã nguồn (ví dụ: ["Claim Mail"] = true, ["Auto Plant"] = true).
2. Các danh sách / Bảng (table) để trống `{}`:
   - ["Favorite"] = {} -> Không tự động khóa yêu thích bất cứ trái cây nào.
   - ["Blacklist Seed"] = {} -> Không cấm trồng loại hạt nào.
   - ["Blacklist Shovel"] = {} -> Không bảo vệ cây nào khỏi bị đào (Cực kỳ nguy hiểm nếu bật Auto Plant vì bot có thể đào mất cây hiếm của bạn).
   - ["Shovel Plant Once"] = {} -> Không thực hiện đào dọn dẹp khi khởi động script.
   - ["Buy Pets"] = {} -> Không mua thêm bất kỳ pet nào từ bản đồ.
   - ["Equip Pets"] = {} -> Không tự động quản lý đeo/gỡ pet (giữ nguyên trạng thái đeo hiện tại).
   - ["Buy Gear"] = {} / ["Gears To Use"] = {} -> Không tự động mua gear / không tự động đeo gear tưới nước.
   - ["Items To Mail"] = {} -> Tắt hoàn toàn tính năng tự động gửi mail.
3. Webhook URL để trống `""`: Tắt hoàn toàn tính năng gửi thông báo Discord tương ứng.

## Cấu hình mẫu

```lua
setfpscap(5)
script_key = "xxx";
getgenv().UserConfig = {
    ["FPS Cap"] = 5,
    ["Auto Buy Seed"] = true,
    ["Auto Plant Seed"] = true,
    ["Limit Plant Seed"] = {
        ["Carrot"] = 50, 
    },
    ["Limit Buy Seed"] = {
        ["Carrot"] = 5, 
        ["Strawberry"] = 5,
        ["Blueberry"] = 5,
        ["Tulip"] = 5,
        ["Tomato"] = 5,
        ["Apple"] = 5,
        ["Bamboo"] = 9999,
        ["Corn"] = 5,
        ["Cactus"] = 5,
        ["Pineangle"] = 5,
        ["Mushroom"] = 9999,
        ["Green Bean"] = 5,
        ["Banana"] = 2,
        ["Grape"] = 2,
        ["Coconut"] = 2,
        ["Mango"] = 2,
        ["Dragon Fruit"] = 2,
        ["Acorn"] = 2,
        ["Cherry"] = 2,
        ["Sunflower"] = 2,
        ["Venus Fly Trap"] = 2,
        ["Pomegranate"] = 2,
        ["Poison Apple"] = 2,
        ["Venom Spitter"] = 10,
        ["Moon Bloom"] = 100,
        ["Dragon's Breath"] = 100,
    },
["Blacklist Shovel"] = {"Dragon's Breath", "Moon Bloom", "Ghost Pepper", "Venom Spitter", "Poison Apple", "Pomegranate", "Venus Fly Trap"},
["Shovel Plant Once"] = {},
    ["Favorite"] = {
        -- ["Horned Melon"] = {"Rainbow", "Gold"},
    },
["Harvest Mutation Only"] = {
        --"Bamboo",
        --["Tomato"] = {"Rainbow", "Gold", "Bloodlit", "Electric", "Starstruck", "Frozen", "Aurora"},
        --"Apple",
    },
    ["Buy Pets"] = {
        ["Frog"] = {Huge = 99, Rainbow = 99}, -- mua 99 Huge, 99 Rainbow (không mua pet Normal, Big)
        ["Bunny"] = {Huge = 99, Rainbow = 99},
        ["Turtle"] = {Huge = 99, Rainbow = 99},
        ["Owl"] = {Huge = 99, Rainbow = 99},
        ["Deer"] = {Huge = 99, Rainbow = 99},
        ["Robin"] = {Big = 99, Huge = 99, Rainbow = 99},
        ["Bee"] = {Big = 99, Huge = 99, Rainbow = 99},
        ["Monkey"] = 999, -- mua 999 tất cả loại
        ["Golden Dragonfly"] = 999,
        ["Unicorn"] = 999,
        ["Raccoon"] = 999,
        ["Black Dragon"] = 999,
    },
    ["Equip Pets"] = {
        {"Bunny", 5, 3},
    },
    ["Expand Plot"] = true,
    ["Plot Expansions"] = 3,
    ["Unlock Pet Slots"] = 5,
    ["Auto Collect Seed Packs"] = true,
    ["Gears"] = {
        ["Buy Gear"] = {
            -- "Common Watering Can",
            -- "Common Sprinkler",
            -- "Uncommon Sprinkler",
            -- "Rare Sprinkler",
            -- "Legendary Sprinkler",
             ["Super Sprinkler"] = 100,
             ["Super Watering Can"] = 100,
        },
        ["Gears To Use"] = {
            -- "Common Watering Can",
            -- "Common Sprinkler",
            -- "Uncommon Sprinkler",
            -- "Rare Sprinkler",
            -- "Legendary Sprinkler",
            -- "Super Sprinkler",
            -- "Super Watering Can",
        },
    },
        -- WH Pet
    ["Webhook Pet URL"] = "https://discord.com/api/webhooks/x",
    ["Webhook Pet Name"] = {"Golden Dragonfly","Unicorn","Raccoon","Monkey","Bee","Ice Serpent","Robin","Deer"},
    ["Webhook Pet Rarity"] = {"Mythic", "Super", "Secret"},
 	-- WH Seed
    ["Webhook Seed URL"] = "https://discord.com/api/webhooks/x",
    ["Webhook Seed Name"] = {"Rainbow", "Gold", "Mega", "Dragon's Breath", "Hypno Bloom", "Moon Bloom", "Briar Rose", "Venom Spitter", "Poison Apple", "Pomegranate", "Venus Fly Trap"},
    	-- WH Gear
    ["Webhook Gear URL"] = "https://discord.com/api/webhooks/x",
    ["Webhook Gear Name"] = {"Super Sprinkler", "Super Watering Can"},
    ["Webhook Note"] = "Danny",
    ["Discord ID"] = "2298505389115965452",
    ["Mail To Username"] = {"AlexEwout2006"},
    ["Items To Mail"] = {
        ["Pet"] = {
            ["Golden Dragonfly"] = 1,
            ["Unicorn"] = 1,
            ["Raccoon"] = 1,
            ["Monkey"] = 1,
            ["Bee"] = {Normal = 1, Big = 1, Huge = 1, Rainbow = 1, To = "AlexEwout2006"},
            ["Ice Serpent"] = 1,
        },
        ["Seed"] = {
            ["Rainbow"] = 2,
            ["Gold"] = {Amount = 20, To = {"AlexEwout2006", "AlexEwout2006"}}, 
            ["Mega"] = 10,
            ["Mushroom"] = {Amount = 1, To = "AlexEwout2006"},
            ["Dragon's Breath"] = 1,
        },
        ["Gear"] = {
            ["Super Sprinkler"] = 1,
        },
    },
    ["Claim Mail"] = true,
    ["Auto Plant"] = true,
    ["Limit Auto Plant"] = 800,
    ["Blacklist Seed"] = {"Rainbow"}
}
loadstring(game:HttpGet("https://api.luarmor.net/files/v4/loaders/66adeacbfb46c0ea4883aefee367292a.lua"))()
```
