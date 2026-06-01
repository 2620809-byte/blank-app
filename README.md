import streamlit as st
import random

st.title("🏪 마트 계산대 대기열 시뮬레이션")
st.write("산업경영공학 대기행렬 이론 기초 시뮬레이터입니다.")

# 1. 입력 설계 (사용자가 버튼을 누르면 시작)
if st.button("시뮬레이션 시작 (10분 가동)"):
    
    wait_list = []
    queue = 0
    
    st.subheader("⏱️ 실시간 운영 기록 (출력)")
    
    # 2. 반복문 가동
    for minute in range(1, 11):
        # 3. 조건문 판정 (확률 데이터 입력 및 처리)
        if random.random() < 0.5:
            queue += 1
            arrival_text = "🟢 새로운 손님 도착"
        else:
            arrival_text = "⚪ 새로 온 손님 없음"
            
        if queue > 0 and random.random() < 0.6:
            queue -= 1
            service_text = "🔵 계산 완료 및 퇴장"
        elif queue > 0:
            service_text = "🟡 아직 계산 중"
        else:
            service_text = "⚪ 계산대 비어 있음"
            
        wait_list.append(queue)
        
        # 화면에 실시간 상황 출력
        st.text(f"[{minute}분] {arrival_text} | {service_text} ➡️ (현재 대기자: {queue}명)")
        
    # 4. 최종 결과 분석 출력
    st.markdown("---")
    st.subheader("📊 최종 통계 분석 결과 (출력)")
    
    col1, col2 = st.columns(2)
    with col1:
        st.metric(label="최대 대기 인원", value=f"{max(wait_list)} 명")
    with col2:
        st.metric(label="평균 대기 인원", value=f"{sum(wait_list)/10:.1f} 명")
        
    # 라인 차트로 시각화 출력
    st.line_chart(wait_list)