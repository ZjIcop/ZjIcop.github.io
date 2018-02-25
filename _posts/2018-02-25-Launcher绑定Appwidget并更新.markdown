``java
//如果需要Appwdiget可以及时的更新，必须需要有一方为系统级应用（Launcher或者Appwdiget)

private AppWidgetManager mAppWidgetManager;
private AppWidgetHost mAppWidgetHost;
private static final int APPWIDGET_HOST_ID = 0x100;

//需要进行初始化
mAppWidgetManager = AppWidgetManager.getInstance(this);
mAppWidgetHost = new AppWidgetHost(getApplicationContext(), APPWIDGET_HOST_ID);

int appWidgetId = mAppWidgetHost.allocateAppWidgetId();
//bindAppWidgetIdIfAllowed 为必须需要执行的，方案有2种，1是程序为系统签名。2是通过反射的方式得到 不绑定无法及时更新
boolean isBinded = mAppWidgetManager.bindAppWidgetIdIfAllowed(appWidgetId, appWidgetProviderInfo.provider);
if (isBinded) {
    i("TAG", left + "-" + with + "绑定成功！");
    appwidgetIdList.add(appWidgetId);
    View hostView = mAppWidgetHost.createView(this, appWidgetId, appWidgetProviderInfo);
    //得到相应的View，并且增加进去即可
    return true;
} else {
    i("TAG", "绑定失败！");
}
``