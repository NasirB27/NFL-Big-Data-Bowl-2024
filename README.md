# NFL-Big-Data-Bowl-2024
def calculate_play_impact(play):
    score = 0
    # Yards Gained/Loss
    score += normalize(play['playResult'], 1, 10)
    # Turnover Impact
    if play['turnover']:
        score += 10
    # First Down Impact
    if play['firstDown']:
        score += 5
    # Scoring Play Impact
    if play['scoringPlay']:
        score += 10
    # Penalty Impact
    score += penalty_impact(play['penaltyYards'])
    # Win/Loss Impact
    score += win_loss_impact(play['winningPlay'])
    # Field Position Impact
    score += field_position_impact(play['fieldPosition'])
    # Quarter Impact
    score += quarter_impact(play['quarter'])
    # Time Impact
    score += time_impact(play['timeRemaining'])
    # Normalize the score to a 1-10 scale
    return min(max(score / max_possible_score * 10, 1), 10)

plays_df['PlayImpactScore'] = plays_df.apply(calculate_play_impact, axis=1)
