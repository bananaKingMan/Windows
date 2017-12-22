//# Windows
//1day Create Window Code

#include <Windows.h>
//定义窗口处理函数（自定义， 处理消息）
LRESULT CALLBACK WndProc(HWND hWnd, UINT msgId, WPARAM wParam, LPARAM lParam)
{
	return DefWindowProc (hWnd, msgId, wParam, lParam);//给各种消息做默认处理
}
//定义WinMain函数
int CALLBACK WinMain (HINSTANCE hIns, HINSTANCE hPreIns, LPSTR IpCmdLine, int nCmdShow)
{
	//3.注册窗口类
	WNDCLASS wc = {0};
	wc.cbClsExtra = 0;
	wc.cbWndExtra = 0;
	wc.hbrBackground = (HBRUSH)(COLOR_WINDOW+1);
	wc.hCursor = NULL;
	wc.hIcon = NULL;
	wc.hInstance = hIns;
	wc.lpfnWndProc = WndProc;
	wc.lpszClassName = "Main";
	wc.lpszMenuName = NULL;
	wc.style = CS_HREDRAW|CS_VREDRAW;
	RegisterClass(&wc);
	HWND hWnd = CreateWindow("Main", "window", WS_OVERLAPPEDWINDOW, 100, 100, 700, 500, NULL, NULL, hIns, NULL);
	ShowWindow(hWnd, SW_SHOW);
	//消息循环
	MSG nMsg = {0};
	while (GetMessage(&nMsg, NULL, 0, 0))
	{
		//翻译消息
		TranslateMessage(&nMsg);
		//派发消息
		DispatchMessage(&nMsg);
	}
	return 0;
}
