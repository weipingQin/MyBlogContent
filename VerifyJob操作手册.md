������ET���Խű���ʱ��,����ʹ��Verify Job�ķ�ʽ�������ĵ���ĳһ��Case
1.��Verify job��ַ
http://hztdci01.china.nsn-net.net/view/IMP_GIT/job/IMP_ET_VERIFY/
2.��� Build with Parameters


ѡ����λ�ȡRPM��
�����Ҫʹ��TRUNK�ϵİ�������HOW_TO_GET_RPM����������ѡ��wget

�����Ҫʹ�ÿ����ṩ��knife��������HOW_TO_GET_RPM����������ѡ��copy


����rpm���Ļ�ȡ��ַ��commit id
���ʹ��TRUNK�ϵİ������ڵ���������ѡ��wget������TRUNK��job���ҵ������rpm���汾������KNIFE_LINK_OR_COMMIT_ID�ı���������RMP�����������ӡ�
TRUNK���ӣ�
http://hztdci01.china.nsn-net.net/view/IMP_GIT_TRUNK/job/IMP_GIT_TRUNK_RPM_PACKAGE/

���ʹ�ÿ����ṩ��knife�������ڵ���������ѡ��copy������KNIFE_LINK
_OR_COMMIT_ID�ı���������Ӧticket��commit id��

����ET case�Ĳ��԰汾

�����Ҫ����ticket�ϵ�case��������ET_CASE_REFSPEC�ı���������ticket�İ汾�š�
�����Ҫֱ�������Ѿ��ύ��case������ET_CASE_REFSPEC�ı���������������
��������master��֧�����е�case��refs/heads/master
��������17A��֧�����е�case��refs/heads/maintenance/17A
��������ET case������
���ϣ�����е���case����ET_COMMAND�ı���������������
pybot -L trace -t 'case name' -d ./log .
�����������滻Ϊ����Ҫ���е�case���ƣ�
���ϣ������ĳ��suite�����е�case����ET_COMMAND�ı���������������
pybot -L trace -s 'suite name' -d ./log .
�����������滻Ϊ����Ҫ���е�suite���ƣ�
���ϣ������ѹ���������е�case����ET_COMMAND�ı���������������
pybot -L trace --listener RobotListener -e status-debug -e feature-LTE3875* -d ./log .
��ʼ����
�����ʼ�����������build history�п��������ύ�Ĺ������ȴ�������ɾͿɿ���case���н����