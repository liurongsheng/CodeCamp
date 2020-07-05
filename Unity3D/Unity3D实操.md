通过标准
Unity引擎应用初级认证
- 认证形式：线上考试
- 通过标准：满分100分，70分合格
- 考试题型：单选，多选，判断

Unity编程开发初级认证
- 认证形式：实践作品开发+评审
- 通过标准：满分100分，70分合格
- 考试题型：实操题

## 编程开发要求
- 使用C#脚本程序实现功能
- 图形用户界面
- 物理引擎系统
- 光影效果应用
- 角色动作系统
- 地形及导航实现
- 角色AI实现（NPC寻路、战斗AI)

## 小游戏
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class shoot : MonoBehaviour
{
    public float moveSpeed = 5f;
    public Rigidbody bullet;
    public float power = 1500f;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        float h = Input.GetAxis("Horizontal") * Time.deltaTime * moveSpeed;
        float v = Input.GetAxis("Vertical") * Time.deltaTime * moveSpeed;
        transform.Translate(h, v, 0);
        if(Input.GetButtonUp("Fire1")){
            Rigidbody instance  = (Rigidbody)Instantiate(bullet, transform.position, transform.rotation);
            Vector3 fwd = transform.TransformDirection(Vector3.forward);
            instance.AddForce(fwd * power);
        }

    }
}

```

## 地形工具箱
路径：GameObject -- 3D Object -- Terrain
组件名：TerrainScript
设置地形分辨率
分辨率在创建之前设置好，以后再调整可能导致地形上的元素复位

- 升高地形（Raise height）
选择升高地形工具，在地形上移动可以升高地形的高度
按住 Shift 键可降低地形
Brush Size 调节笔触大小
Opacity 调节笔触力度

- 绘制高度（Paint height）
在地形上绘制相同高度的地表
按住Shif键可选择高度（Height）
Brush size 调节笔触大小
Opacity 调节笔触力度
Height 设置高度

- 平滑高度（Smooth Height）
平滑高度用来制作平滑的地形或使两个尖锐的面平滑过渡
Brush size 调节笔触大小
Opacity 调节笔触力度

- 大量放置树木（Mass Place Trees)
用于在地形上快速大量放置树林可以设置一些相关参数width，height，density，and variation），但是不能控制放置树木的位置
通过 Edit Trees按钮可以增加，编辑，移除树木对象
按住 shift 键可以删除已放置在地形的树木
按住 ctrl 键可以根据树木类型来删除已放置在地形树木

- 地形刷新（Refresh）
如果地形元素使用的资产有修改，可使用该工具将修改的内容更新到地形上

- 绘制纹理（Paint Texture）
根据选择的纹理图形，绘制地表，如草地、泥土地等
通过 Edit Textures 按钮可以增加，编辑，移除纹理

- 绘制细节（Paint details）
根据选择的纹理图形，绘制地形细节的游戏对象比如花，草，植物，岩石，叶子等
通过 edit detail 按钮可以增加，编辑，移除纹理

## doorclistion.cs
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class doorclistion : MonoBehaviour
{
	// Start is called before the first frame update
	private bool doorIsOpen = false;
	private float doorTimer = 0.0f;
	public float doorOpenTime = 3.0f;
	public AudioClip doorOpenSound;
	public AudioClip doorShutSound;
	public Text textHints;

	void Start()
	{
		textHints.enabled = false;
	}
	// Update is called once per frame
	void Update()
	{
		if(doorIsOpen){
			doorTimer += Time.deltaTime;
			if(doorTimer > doorOpenTime){
				Door(doorShutSound, false, "doorshut");
				doorTimer = 0.0f;
			}
		}
	}
	void OnTriggerEnter(Collider col){
		if(col.gameObject.tag == "Player"){
			if(Inventory.charge >= 4){
				DoorCheck();
				if(GameObject.Find("PowerGUI")){
					Destroy(GameObject.Find("PowerGUI"));
				}
			}else{
				ShowHint("门锁上了，我们需要收集更多的电池来打开它...");
				StartCoroutine("TextShowHiden");
			}

		}
	}
	void DoorCheck(){
		if(!doorIsOpen){
			Door(doorOpenSound, true, "dooropen");
		}
	}
	// 控制门的开合
	void Door(AudioClip aClip, bool openCheck, string animName){
		GetComponent<AudioSource>().PlayOneShot(aClip);
		doorIsOpen = openCheck;
		transform.parent.gameObject.GetComponent<Animation>().Play(animName);
	}
	void ShowHint(string message){
		textHints.text = message;
		if (!textHints.enabled) {
			textHints.enabled = true;
		}
	}
	IEnumerator TextShowHiden(){
		yield return new WaitForSeconds (4f);
		textHints.enabled = false;
	}
}
```
## powerCell
```
using UnityEngine;
using System.Collections;

public class powerCell : MonoBehaviour {

	// Use this for initialization
	public float rotationSpeed = 100.0f;
	void Start () {
	
	}
	// Update is called once per frame
	void Update () {
		transform.Rotate (new Vector3 (0, rotationSpeed * Time.deltaTime, 0));
	}
	void OnTriggerEnter(Collider col){
		if(col.gameObject.tag == "Player"){
			col.gameObject.SendMessage("CellPickup");
			Destroy(gameObject);
		}
	}
}
```
## Inventory
```
using UnityEngine;
using System.Collections;
using UnityEngine.UI;

public class Inventory : MonoBehaviour {
	public AudioClip collectSound;
	static public int charge = 0; 
	public Sprite[] hudCharge;
	public Image chargeHudGUI;
	public Light doorLight;

	public GameObject generator;
	public Texture[] generatorTexture;
	// Use this for initialization
	void Start () {
	
	}
	
	// Update is called once per frame
	void Update () {
	
	}
	void CellPickup(){
		AudioSource.PlayClipAtPoint (collectSound, transform.position);
		charge++;

		if (charge == 4) {
			doorLight.color = Color.green;
		}
		if (charge <= 4) {
			chargeHudGUI.sprite = hudCharge[charge];
			generator.transform.Find("chargeMeter").GetComponent<Renderer>().material.mainTexture = generatorTexture[charge];
		}
	}
}


```
## 
```
using UnityEngine;
using System.Collections;

public class throwTigger : MonoBehaviour {

	// Use this for initialization
	void Start () {
	
	}
	
	// Update is called once per frame
	void Update () {
	
	}

	void OnTriggerEnter(Collider col){
		if (col.gameObject.tag == "Player") {
			CoconutThrower.canThrow = true;
		}
	}
	void OnTriggerExit(Collider col){
		if (col.gameObject.tag == "Player") {
			CoconutThrower.canThrow = false;
		}
	}
}

```
