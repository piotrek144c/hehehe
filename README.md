using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class PaskiPotrzeb : MonoBehaviour {

	private bool gamePaused = false;
    public float maxZdrowie, obecneZdrowie, maxGlod, obecneGlod, maxPragnienie, obecnePragnienie;
	public GUISkin skin;
	private Canvas manuUI;
		
	// Use this for initialization
	void Start () {	
		maxZdrowie = 100;
        obecneZdrowie = 100;
		maxGlod = 100;
		obecneGlod = 100;
		maxPragnienie = 100;
		obecnePragnienie = 100;
	}
	
	// Update is called once per frame
	void Update () {
		obecneGlod -= 0.07f * Time.deltaTime;
		obecnePragnienie -= 0.1f * Time.deltaTime;
	
		if (obecneGlod <= 0)
		{
			obecneGlod = 0;
			obecneZdrowie -= 1 * Time.deltaTime;
		}
	
		if (obecnePragnienie <= 0)
		{
			obecnePragnienie = 0;
			obecneZdrowie -= 1 * Time.deltaTime;
		}
		
		if (obecneGlod > 0 && obecnePragnienie > 0)
		{
			if (obecneZdrowie < maxZdrowie)
			obecneZdrowie += 0.1f *Time.deltaTime;
		}
		

		if (obecneZdrowie <= 0) {
			obecneZdrowie = 0;
		if (gamePaused) {
		Time.timeScale = 0;
		gamePaused = false;
		} else {
		Time.timeScale = 0;
		gamePaused = true;
		}
		}
	}
	

    private void OnGUI()
    {
        GUI.Box(new Rect(20, Screen.height - 110, 150, 20), "Zdrowie: " + obecneZdrowie.ToString("0.") + "/" + maxZdrowie, skin.GetStyle("PasekZdrowia"));
		GUI.Box(new Rect(20, Screen.height - 50, 150, 20), "Głód: " + obecneGlod.ToString("0.") + "/" + maxGlod, skin.GetStyle("PasekGlodu"));
		GUI.Box(new Rect(20, Screen.height - 80, 150, 20), "Pragnienie: " + obecnePragnienie.ToString("0.") + "/" + maxPragnienie, skin.GetStyle("PasekPragnienia"));
    }
	
}
